# HW3 Part 2: Normalization

# Solutions

## Warmup:
Trivial functional dependencies are those where the right side is included on the left. For example: ABC->C

To derive additional functional dependencies, we can use Armstrong's Axioms:
- Augment the existing functional dependencies by adding attributes to both sides.
- Apply transitivity to other functional dependencies.

**Q2.1**
  * Non trivial functional dependencies (in addition to given FDs): C->B, AC->B, BC->A
  * Keys: C


**Q2.2**
  * Non trivial functional dependencies (in addition to given FDs):
    - AB->D,
    - BC->A,
    - AD->C,
    - CD->B,
    - ABC->D,
    - ABD->C,
    - BCD->A,
    - ACD->B

  * Keys: AB, BC, CD, AD

# Real application:
**Q2.3**

Key in `iowa` -
`(store, itemno, date, vendor_no, invoice_line_no)`


**Q2.4**

We compute the min cover and get the following:

- store → address,
- store → name,
- store → city,
- store → zipcode,
- store → store_location,
- store → county_number,
- store → county,
- store → store_location_address,
- store → store_location_city,
- store → store_location_zip
- vendor_no → vendor
- category → category_name
- itemno → category,
- itemno → bottle_volume_ml,
- itemno → im_desc,
- itemno → state_bottle_cost,
- itemno → state_bottle_retail
- date, store, vendor_no, itemno, invoice_line_no → pack,
- date, store, vendor_no, itemno, invoice_line_no → sale_bottles,
- date, store, vendor_no, itemno, invoice_line_no → sale_dollars,
- date, store, vendor_no, itemno, invoice_line_no → sale_gallons,
- date, store, vendor_no, itemno, invoice_line_no → sale_liters

Note that we already have a min cover so we obtain the following schema decomposition:
 * ` <store, address, name, city, zipcode, store_location, county_number, county, store_location_address, store_location_city, store_location_zip> `
 * ` <vendor_no,vendor> `
 * ` <category,category_name> `
 * ` <itemno, category, bottle_volume_ml, im_desc, state_bottle_cost, state_bottle_retail> `
 * ` <date, store, vendor_no, itemno, invoice_line_no, pack, sale_bottles, sale_dollars, sale_gallons, sale_liters> `


**Q2.5**

It can be observed that running BCNF using min cover, that there are no additional tables required and the final schema decomposition is thus redundancy and anomaly free in this particular case given the set of FDs. In general, a decomposition into 3NF will not be always be redundancy-free and will permit anomalies.

**Q2.6**

**False.** The constraint given in the question is a check constraint, that only involves the value of a single column. Functional dependencies cannot enforce check constraints. They can only enforce a relationship between the values in two or more columns.


**Q2.7** `select distinct(vendor) from iowa where itemno = '3326';`

**Result:**

  We find only one vendor: `Bacardi U.S.A., Inc.`

**Q2.8**

**No,** the `itemno` and `vendor_name` should not have a functional dependency. The design of the database may seem that the `itemno` uniquely identifies a `vendor_name`, meaning one `vendor_name` name given a `itemno` number. However, if we run the following query:

```sql
select i1.itemno, i1.vendor_name, i2.vendor_name
from iowa i1, iowa i2
where i1.itemno = i2.itemno and i1.vendor_name <> i2.vendor_name
```

We'll find instances where the `itemno` is equivalent, but we have different vendor names. For example, `itemno=4936` has record with two vendor names: `MHW Ltd ...` and `Edrington Group USA LLC ...`.

This just proves the dangers of redundancy. Since the facts about the mapping between `itemno -> vendor_name` were recorded multiple times, it introduced the opportunity for errors, as demonstrated by the values above.
