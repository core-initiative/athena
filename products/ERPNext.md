## ERP Next Customization
### 1. Customize Party Type
Problem:
- We can not add party type
- We can not add party type with the same party

Solution:
1. Enable ERPNext developer_mode
```bash
# navigate to frappe_bench directory first
$ bench config -g developer_mode 1
$ bench --site <site-name> clear-cache
$ bench setup requirements --dev
```
2. Open DocType `Party Type` 
  - Edit field `party_type` remove the `Unique` constraint
  - Change the `Naming` rule to expression : `{party_type}-{accoount_type}`
  - Uncheck `User Can Not Create`

Now you should be able to add new `Party Type`

### 2. Use locale ID but with english translation
Problem: 
- We want to have a currency in IDR and the word in Indonesian but the system language stay with English

Solution
1. Go to your `frappe_bench` directory
2. Navigate to directory `apps/frappe/frappe/translation`
  - Rename the original file `id.csv` to `id.csv.orig`
  - Copy the file `en_us.csv` as `id.csv`
3. Navigate to directory `apps/erpnext/erpnext/translation`
  - Rename the original file `id.csv` to `id.csv.orig`
  - Copy the file `en_us.csv` as `id.csv`