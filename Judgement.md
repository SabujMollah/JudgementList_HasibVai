
## Judgement List (View Mode)

### c1: **Person in Charge (担当者)**

- **Header Label:** `Person in Charge (担当者)`
- **Data Type:** `String`
- **Custom render:** `String`
- **Source:**
  The employee name is retrieved based on the employee_id from either the T_HANTEI or RSOS_T_PRODUCT_ORDER table. If the employee_id matches a record in either table in the given order, the corresponding employee_name is returned
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the name of the person in charge, retrieved from the T_HANTEI or RSOS_T_PRODUCT_ORDER table.

---

### c2: **In-house/Outsourcing (内製/外製)**

- **Header Label:** `In-house/Outsourcing (内製/外製)`
- **Data Type:** `TinyInt`
- **Custom render:**
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=1)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**
  The in-house or outsourcing text value is selected from the M_DISPLAY_ITEM table. `T_HANTEI` table contains ITEM_NO, which is available inside the `M_DISPLAY_ITEM` table. By matching the result with ITEM_NO, it displays an item that corresponds to either in-house or outsourcing, with the options defined as: 0: 内製 (in-house), 1: 外製 (outsourcing)
- **Save Destination:** `N/A` (Not editable)
- **Validation:** Show only text values from the `M_DISPLAY_ITEM` table that are matched with `T_HANTEI.ITEM_NO` and `M_DISPLAY_ITEM.ITEM_NO`.
- **Options:** `N/A`
- **Remarks:** Displays whether the product is in-house or outsourced. Value is fixed at 0 for in-house.

---

### c3: **Reference Item CD (基準品目CD)**

- **Header Label:** `Reference Item CD (基準品目CD)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
  The `ITEM_CODE` is retrieved from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. The `ITEM_CODE` is returned as the reference item CD.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the reference item code, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c4: **Production Abbreviation (生産略称)**

- **Header Label:** `Production Abbreviation (生産略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
  The `PRODUCT_SHORT_NAME` is retrieved from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. The PRODUCT_SHORT_NAME is returned as the production abbreviation.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the production abbreviation, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c5: **Sales Abbreviation (販売略称)**

- **Header Label:** `Sales Abbreviation (販売略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
  The sales abbreviation is retrieved from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. `The SALES_SHORT_NAME` is returned as the sales abbreviation.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the sales abbreviation, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c6: **Lot (ロット)**

- **Header Label:** `Lot (ロット)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
 The lot number is fetched from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. The `LOT_NO` is returned as the lot number.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the lot number, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c7: **Delivery Date (納品日)**

- **Header Label:** `Delivery Date (納品日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**
  The delivery date is fetched from the `RSOS_T_PRODUCT_ORDER` table by matching the `ORDER_ID`. The `DELIVERY_DATE` is returned as the delivery date.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the delivery date, fetched from the RSOS_T_PRODUCT_ORDER table.

---

### c8: **Production Building/Outsourcing (生産棟/外製先)**

- **Header Label:** `Production Building/Outsourcing (生産棟/外製先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
  The production building or outsourcing location is retrieved from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. The `PRODUCT_PLACE_NAME` is returned as the location.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the name of the production building or outsourcing location, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c9: **Item Name (品目名称)**

- **Header Label:** `Item Name (品目名称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
  The item name is fetched from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. The `ITEM_NAME` is returned as the item name.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the item name, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c10: **Date of Dispensing (調合日)**

- **Header Label:** `Date of Dispensing (調合日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**
   The date of dispensing is acquired through recursive processing based on the item’s order code from `RSOS_T_ORDERS_RELATION`, `RSOS_T_PRODUCT_RECORD`, and `RSOS_T_PRODUCT_ORDER`. It considers the maximum `END_DATE` from `RSOS_T_PRODUCT_RECORD` or `END_SCH_DATE` from `RSOS_T_PRODUCT_ORDER` where the process type in `RSOS_M_PROCESSES` is '1'.
   ```sql
  (SELECT JSON_OBJECT(
                        'c10', MAX(CASE WHEN KO.PROCESS_TYPE = '1' THEN IFNULL(SJ.END_DATE, SO.END_SCH_DATE) ELSE NULL END)                      
                    ) FROM RSOS_T_ORDERS_RELATION r
                    LEFT JOIN RSOS_T_PRODUCT_RECORD SJ ON r.PRE_ORDER_CODE = SJ.ORDER_CODE
                    LEFT JOIN RSOS_T_PRODUCT_ORDER SO ON r.PRE_ORDER_CODE = SO.ORDER_CODE
                    LEFT JOIN RSOS_M_PROCESSES KO ON SO.PLANT_ITEM_CODE = KO.GRAPH_CODE
                        AND SO.OPERATION_ORG_DIV = KO.GRAPH_SELECTOR
                        AND SO.PROC_CODE = KO.PROC_CODE
                    WHERE r.FLW_ORDER_CODE = RSOS_V_JUDGE_PRODUCT.ORDER_CODE
                    ) AS process_dates
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the date of dispensing, acquired through recursive processing.

---

### c11: **Filling Date (充填日)**

- **Header Label:** `Filling Date (充填日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**
   The filling date is acquired through recursive processing based on the item’s order code from `RSOS_T_ORDERS_RELATION`, `RSOS_T_PRODUCT_RECORD`, and `RSOS_T_PRODUCT_ORDER`. It considers the maximum `END_DATE` from `RSOS_T_PRODUCT_RECORD` or `END_SCH_DATE` from `RSOS_T_PRODUCT_ORDER` where the process type in `RSOS_M_PROCESSES` is '2'.
   ```sql
  (SELECT JSON_OBJECT(                    
                        'c11', MAX(CASE WHEN KO.PROCESS_TYPE = '2' THEN IFNULL(SJ.END_DATE, SO.END_SCH_DATE) ELSE NULL END),
                    ) FROM RSOS_T_ORDERS_RELATION r
                    LEFT JOIN RSOS_T_PRODUCT_RECORD SJ ON r.PRE_ORDER_CODE = SJ.ORDER_CODE
                    LEFT JOIN RSOS_T_PRODUCT_ORDER SO ON r.PRE_ORDER_CODE = SO.ORDER_CODE
                    LEFT JOIN RSOS_M_PROCESSES KO ON SO.PLANT_ITEM_CODE = KO.GRAPH_CODE
                        AND SO.OPERATION_ORG_DIV = KO.GRAPH_SELECTOR
                        AND SO.PROC_CODE = KO.PROC_CODE
                    WHERE r.FLW_ORDER_CODE = RSOS_V_JUDGE_PRODUCT.ORDER_CODE
                    ) AS process_dates
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the filling date, acquired through recursive processing.

---

### c12: **Packing Date (包装日)**

- **Header Label:** `Packing Date (包装日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The packing date is acquired through recursive processing based on the item’s order code from `RSOS_T_ORDERS_RELATION`, `RSOS_T_PRODUCT_RECORD`, and `RSOS_T_PRODUCT_ORDER`. It considers the maximum `END_DATE` from `RSOS_T_PRODUCT_RECORD` or `END_SCH_DATE` from `RSOS_T_PRODUCT_ORDER` where the process type in `RSOS_M_PROCESSES` is '3'.
  ```sql
  (SELECT JSON_OBJECT(
                        'c12', MAX(CASE WHEN KO.PROCESS_TYPE = '3' THEN IFNULL(SJ.END_DATE, SO.END_SCH_DATE) ELSE NULL END)
                    ) FROM RSOS_T_ORDERS_RELATION r
                    LEFT JOIN RSOS_T_PRODUCT_RECORD SJ ON r.PRE_ORDER_CODE = SJ.ORDER_CODE
                    LEFT JOIN RSOS_T_PRODUCT_ORDER SO ON r.PRE_ORDER_CODE = SO.ORDER_CODE
                    LEFT JOIN RSOS_M_PROCESSES KO ON SO.PLANT_ITEM_CODE = KO.GRAPH_CODE
                        AND SO.OPERATION_ORG_DIV = KO.GRAPH_SELECTOR
                        AND SO.PROC_CODE = KO.PROC_CODE
                    WHERE r.FLW_ORDER_CODE = RSOS_V_JUDGE_PRODUCT.ORDER_CODE
                    ) AS process_dates
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the packing date, acquired through recursive processing.

---

### c13: **Planned Quantity (予定数量)**

- **Header Label:** `Planned Quantity (予定数量)`
- **Data Type:** `Decimal`
- **Custom render:** `Decimal`
- **Source:**  
  The planned quantity is fetched from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. It considers `RECORD_QTY` if `END_DATE` is valid, otherwise, it returns `QTY`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the planned quantity. If `RSOS_V_JUDGE_PRODUCT.END_DATE` and `RECORD_QTY` are valid, `RECORD_QTY` is shown; otherwise, `QTY` is displayed.

---

### c14: **Usual Judgment Day (通常判定日)**

- **Header Label:** `Usual Judgment Day (通常判定日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The usual judgment day is fetched from the `RSOS_V_JUDGE_PRODUCT` table by matching the `ITEM_ID`. It returns the `SHIP_JUDGE_SCH_DATE` as the judgment day.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the usual judgment day, fetched from the `RSOS_V_JUDGE_PRODUCT` table.

---

### c15: **Test Status (試験ステータス)**

- **Header Label:** `Test Status (試験ステータス)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**  
  The test status is fetched from the `RSOS_T_PRODUCT_ORDER` table by matching the `ORDER_ID`. It returns `QC_STATUS`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `Display acquired values (codes) as they are`
- **Options:** `N/A`
- **Remarks:** Displays the test status, fetched from the `RSOS_T_PRODUCT_ORDER` table.

---

### c16: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=2)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**  
  The urgent sign is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_TYPE`.
- **Save Destination:** `T_HANTEI.URGENT_TYPE`
- **Validation:** `Input required when急ぎ依頼日(the date of urgent request), 急ぎ判定希望日(desired date of urgent judgment)・希望時間(desired time for urgent judgment)are input.`
- **Options:** `N/A`
- **Remarks:** Displays the urgent sign, fetched from the `T_HANTEI` table.

---

### c17: **Urgent Request Date (急ぎ依頼日)**

- **Header Label:** `Urgent Request Date (急ぎ依頼日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The urgent request date is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_REQ_DATE`.
- **Save Destination:** `T_HANTEI.URGENT_REQ_DATE`
- **Validation:** `Set today's date when setting「急ぎサイン」(c16). Required when input 「急ぎサイン」(c16).`
- **Options:** `N/A`
- **Remarks:** Displays the urgent request date, fetched from the `T_HANTEI` table.

---

### c18: **Desired Date of Urgent Judgment (急ぎ判定希望日)**

- **Header Label:** `Desired Date of Urgent Judgment (急ぎ判定希望日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The desired date of urgent judgment is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_JUDGE_REQ_DATE`.
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_DATE`
- **Validation:** `When the「急ぎサイン」(c16) is other than 「1=急」(1=urgent), input is not possible. Required when「急ぎサイン」(c16) is「1=急」(1=urgent).`
- **Options:** `N/A`
- **Remarks:** Displays the desired date for urgent judgment, fetched from the `T_HANTEI` table.

---

### c19: **Desired Time for Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time for Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=4)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**  
  The desired time for urgent judgment is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_JUDGE_REQ_TIME`.
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_TIME`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the desired time for urgent judgment, fetched from the `T_HANTEI` table.

---

### c20: **Reply of Quality Department (品質部門の返信)**

- **Header Label:** `Reply of Quality Department (品質部門の返信)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**  
  The reply from the quality department is fetched from the `T_RESPONSE` table by matching the `RESPONSE_ID`. It returns `URGENT_JUDGE_RESP`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the reply from the quality department, fetched from the `T_RESPONSE` table.

---

### c21: **Revision Judgment Date (修正判定日)**

- **Header Label:** `Revision Judgment Date (修正判定日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The revision judgment date is fetched from the `T_RESPONSE` table by matching the `RESPONSE_ID`. It returns `URGENT_JUDGE_RESP_ANS_DATE`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When 修正判定時間(for c21)=1, display c21 + "AM". Otherwise, display c21.`
- **Options:** `N/A`
- **Remarks:** Displays the revision judgment date, fetched from the `T_RESPONSE` table.


---

### c23: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=12)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**  
  The attributes are fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_ATTRIBUTE`.
- **Save Destination:** `T_HANTEI.URGENT_ATTRIBUTE`
- **Validation:** `When「急ぎサイン」(c16) is 「1=急」 (1=urgent), input required.`
- **Options:** `N/A`
- **Remarks:** Displays the attributes, fetched from the `T_HANTEI` table.

---

### c24: **Desired Movement Date (移動希望日)**

- **Header Label:** `Desired Movement Date (移動希望日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  - If the plant division name in the RSOS_V_JUDGE_PRODUCT table is '大阪' and the urgent type in the T_HANTEI table is 1, check if the plant division name or location in the T_HANTEI or RSOS_M_LOCATION tables is either '梅田倉庫' or 'トランスシティ'.
  - If the condition is met, and the response answer date (URGENT_JUDGE_RESP_ANS_DATE) in the T_RESPONSE table or the urgent judge request date (URGENT_JUDGE_REQ_DATE) in the T_HANTEI table exists, calculate the maximum date (FDATE) from the ERP_CALEM table where the date (FDATE) is greater than either the response answer date or request date, considering working days (FHOLIDAYFLG = 'W').
  - If the plant division is '上野工場' or not '大阪', no movement date is calculated.
  - If the urgent type in the T_HANTEI table is not 1, calculate based on other conditions by considering plant division name or location and response time from the T_RESPONSE table.
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '大阪' AND T_HANTEI.URGENT_TYPE = 1 THEN
                            CASE
                                WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                        ELSE
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                    END
                                ELSE
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN
                                            COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE)
                                        ELSE
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                    END
                            END
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '上野工場' OR RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME <> '大阪' THEN
                            NULL
                        ELSE
                            CASE
                                WHEN T_HANTEI.URGENT_TYPE != 1 THEN
                                    CASE
                                        WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                                ELSE
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 3) AS DATE_LIST)
                                            END
                                        ELSE
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                                ELSE
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                            END
                                    END
                                ELSE
                                    NULL
                            END
                    END AS MOVE_REQ_DATE
  ```
- **Save Destination:** `T_HANTEI.MOVE_REQ_DATE`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the desired movement date, calculated based on predefined logic.

---

### c25: **Evening Packing・Morning Delivery Sign (宵積サイン)**

- **Header Label:** `Evening Packing・Morning Delivery Sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(AM/PM)` 1= AM, 0=PM
- **Source:**  
   1. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '大阪' and the urgent type in the `T_HANTEI` table is 1, then:
     - Check if the plant division name or location in the `T_HANTEI` or `RSOS_M_LOCATION` tables is either '梅田倉庫' or 'トランスシティ'.
     - If the response answer date (`URGENT_JUDGE_RESP_ANS_DATE`) in the `T_RESPONSE` table or the urgent judge request date (`URGENT_JUDGE_REQ_DATE`) in the `T_HANTEI` table is present and the response answer time or request time is 1, then return 0; otherwise, return 1.
  
  2. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '上野工場' or any value other than '大阪', return 0.

  3. If the urgent type in the `T_HANTEI` table is not 1, similar logic is applied based on the plant division name, urgent judge request date, and response times from the `T_RESPONSE` table.

  This logic uses data from `RSOS_V_JUDGE_PRODUCT`, `T_HANTEI`, `T_RESPONSE`, and `RSOS_M_LOCATION` tables to determine if the evening packing or morning delivery sign should be flagged (0 or 1).
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '大阪' AND T_HANTEI.URGENT_TYPE = 1 THEN
                            CASE
                                WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN 0 ELSE 0
                                    END
                                ELSE
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN 1 ELSE 0
                                    END
                            END
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '上野工場' OR RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME <> '大阪' THEN
                            0
                        ELSE
                            CASE
                                WHEN T_HANTEI.URGENT_TYPE != 1 THEN
                                    CASE
                                        WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN 0 ELSE 0
                                            END
                                        ELSE
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN 1 ELSE 0
                                            END
                                    END
                                ELSE
                                    0
                            END
                    END AS VESPER_FLAG
  ```
- **Save Destination:** `T_HANTEI.VESPER_FLAG`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the evening packing or morning delivery sign, calculated based on predefined logic.

---

### c26: **Usual Available Date for Shipment (通常出荷可能日)**

- **Header Label:** `Usual Available Date for Shipment (通常出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
   1. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '上野' and the `RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV` matches the operation org division in the `M_BUILDING_C` table:
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the calendar type (`FCALETYP`) is 'A', the date is after the scheduled shipment judge date (`SHIP_JUDGE_SCH_DATE`) from `RSOS_V_JUDGE_PRODUCT`, and the holiday flag (`FHOLIDAYFLG`) is 'W'.
     - Limit the result to the first 6 dates.

  2. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '大阪':
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the conditions are the same as above but limit the result to the first 3 dates.

  3. For all other plant division names:
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the conditions are the same as above but limit the result to the first 2 dates.
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '上野'
                            AND RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV = (SELECT OPERATION_ORG_DIV FROM M_BUILDING_C WHERE RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV = M_BUILDING_C.OPERATION_ORG_DIV)
                        THEN (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE > RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE ASC
                                LIMIT 6
                            ) AS DATE_LIST
                        )
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '大阪' THEN (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE > RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE ASC
                                LIMIT 3
                            ) AS DATE_LIST
                        )
                        ELSE (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE > RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE ASC
                                LIMIT 2
                            ) AS DATE_LIST
                        )
                    END AS c26
  ```

- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the usual available date for shipment, calculated based on predefined logic.

---

### c27: **Available Date for Express Shipment (急ぎ出荷可能日)**

- **Header Label:** `Available Date for Express Shipment (急ぎ出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  1. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is either '大阪' or '上野' and the `RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV` matches the operation org division in the `M_BUILDING_C` table:
     - If `T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE` is not null, use the `T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME`. If `T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE` is null but `T_HANTEI.URGENT_JUDGE_REQ_DATE` is available, use `T_HANTEI.URGENT_JUDGE_REQ_TIME`.
     - If the urgent judgment response time is 1, select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the calendar type (`FCALETYP`) is 'A', the date is after the urgent judgment response or request date (`T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE` or `T_HANTEI.URGENT_JUDGE_REQ_DATE`), and the holiday flag (`FHOLIDAYFLG`) is 'W'. Limit the result to the first 1 date.
     - Otherwise, limit the result to the first 2 dates.

  2. For all other plant division names:
     - If the urgent judgment response time is 1, select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the same conditions apply but limit the result to the first 2 dates.
     - Otherwise, limit the result to the first 3 dates.
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION = '大阪' OR
                            (RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION = '上野' AND
                            RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV = (SELECT OPERATION_ORG_DIV FROM M_BUILDING_C WHERE RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV = M_BUILDING_C.OPERATION_ORG_DIV))
                        THEN
                            CASE
                                WHEN (CASE
                                            WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                            WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                            ELSE 0
                                        END) = 1 THEN
                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE, T_HANTEI.URGENT_JUDGE_REQ_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                ELSE
                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE, T_HANTEI.URGENT_JUDGE_REQ_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                            END
                        ELSE
                            CASE
                                WHEN (CASE
                                            WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                            WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                            ELSE 0
                                        END) = 1 THEN
                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE, T_HANTEI.URGENT_JUDGE_REQ_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                ELSE
                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE, T_HANTEI.URGENT_JUDGE_REQ_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 3) AS DATE_LIST)
                            END
                    END AS c27
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the available date for express shipment, calculated based on predefined logic.

---

### c28: **Available Date for Loose Shipment (緩め出荷可能日)**

- **Header Label:** `Available Date for Loose Shipment (緩め出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The available date for loose shipment is fetched from the `T_NONURGENT_SHIPMENT` table by matching the `SHIPMENT_ID`. It returns the `LATE_SHIP_POSSIBLE_DATE`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the available date for loose shipment, fetched from the `T_NONURGENT_SHIPMENT` table.

---

### c29: **Desired Date of Loose Judgment (緩め判定希望日)**

- **Header Label:** `Desired Date of Loose Judgment (緩め判定希望日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  1. If `T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE` is `NULL`, the result is `NULL`.
  
  2. If `T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE` is not `NULL` and the plant division in `RSOS_V_JUDGE_PRODUCT` is '大阪':
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table, where the calendar type (`FCALETYP`) is 'A', the date is on or before the late ship possible date (`T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE`), and the holiday flag (`FHOLIDAYFLG`) is 'W'. Limit the result to the last 3 dates.
  
  3. If `T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE` is not `NULL` and the plant division in `RSOS_V_JUDGE_PRODUCT` is '上野':
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table under the same conditions as above, but limit the result to the last 6 dates.
  
  4. For all other cases where `T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE` is not `NULL`:
     - Select the maximum future date (`FDATE`) from the `ERP_CALEM` table, but limit the result to the last 2 dates.
  ```sql
  CASE
                        WHEN T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE IS NULL THEN NULL
                        WHEN T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE IS NOT NULL AND RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION = '大阪' THEN (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE <= T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE DESC
                                LIMIT 3
                            ) AS DATE_LIST
                        )
                        WHEN T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE IS NOT NULL AND RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION = '上野' THEN (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE <= T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE DESC
                                LIMIT 6
                            ) AS DATE_LIST
                        )
                        ELSE (
                            SELECT MAX(FDATE) FROM (
                                SELECT FDATE FROM ERP_CALEM
                                WHERE FCALETYP = 'A'
                                AND FDATE <= T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE
                                AND FHOLIDAYFLG = 'W'
                                ORDER BY FDATE DESC
                                LIMIT 2
                            ) AS DATE_LIST
                        )
                    END AS c29
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When the「急ぎサイン」(c16) is other than 「2=緩」(2=loose), input is not possible. Input required when 「急ぎサイン」(c16) is「2=緩」(2=loose).`
- **Options:** `N/A`
- **Remarks:** Displays the desired date of loose judgment, fetched from the `T_NONURGENT_SHIPMENT` table.

---

### c30: **Desired Time of Loose Judgment (緩め判定希望時間)**

- **Header Label:** `Desired Time of Loose Judgment (緩め判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**  
  1. If `T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE` is `NULL`, the result is `0`.

  2. In all other cases, the result is also `0`.
```sql
  CASE
                        WHEN T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE IS NULL THEN 0
                        ELSE 0
                    END AS c30
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When the「急ぎサイン」(c16) is other than 「2=緩」(2=loose), input is not possible.`
- **Options:** `N/A`
- **Remarks:** Displays the desired time of loose judgment, fetched from the `T_NONURGENT_SHIPMENT` table.

---

### c31: **Destination/Delivery (移動先/納品先)**

- **Header Label:** `Destination/Delivery (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**  
    1. If `RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV` matches the `OPERATION_ORG_DIV` from the `M_BUILDING_C` table, a JSON array of values from `M_DISPLAY_ITEM` where `ITEM_NO = 13` is selected.

  2. If there is no match, the destination name is fetched from `RSOS_M_LOCATION` based on the `LOCATION_CODE` of the `RSOS_T_PRODUCT_ORDER.INVENTORY_LOCATION`.
 ```sql
  (CASE
                        WHEN RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV = (
                            SELECT OPERATION_ORG_DIV
                            FROM M_BUILDING_C
                            WHERE M_BUILDING_C.OPERATION_ORG_DIV = RSOS_T_PRODUCT_ORDER.OPERATION_ORG_DIV
                            LIMIT 1
                        )
                        THEN (
                            SELECT JSON_ARRAYAGG(VALUE)
                            FROM M_DISPLAY_ITEM
                            WHERE ITEM_NO = 13
                        )
                        ELSE (
                            SELECT LOCATION_NAME
                            FROM RSOS_M_LOCATION
                            WHERE LOCATION_CODE = RSOS_T_PRODUCT_ORDER.INVENTORY_LOCATION
                            LIMIT 1
                        )
                    END) AS DELIVERY_DESTINATION
  ```
- **Save Destination:** `T_HANTEI.DELIVERY_DESTINATION_NAME`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the destination or delivery name. If no data in `T_HANTEI`, it is fetched from `RSOS_M_LOCATION`.

---

### c32: **Number of Pallets (パレット数)**

- **Header Label:** `Number of Pallets (パレット数)`
- **Data Type:** `Integer`
- **Custom render:** `Integer`
- **Source:**  
  1. If `USD.FUSRDEC2`, `USD.FUSRDEC3`, or `USD.FUSRDEC3 = 0` is null, the result is `NULL`.
  
  2. If the above condition is not met, the number of pallets is calculated as the ceiling of the division of the product quantity (`RSOS_V_JUDGE_PRODUCT.QTY`) by the pallet size. The pallet size is determined by:
     - If `STD.SKORIIRISU` is not null and greater than 0, it is used.
     - Otherwise, `USD.FUSRDEC2` is used.
  
  The division result is further divided by `USD.FUSRDEC3` to calculate the final number of pallets.
  ```sql
  CASE
                        WHEN USD.FUSRDEC2 IS NULL OR USD.FUSRDEC3 IS NULL OR USD.FUSRDEC3 = 0 THEN NULL
                        ELSE CEILING(
                            RSOS_V_JUDGE_PRODUCT.QTY /
                            (CASE
                                WHEN STD.SKORIIRISU IS NOT NULL AND STD.SKORIIRISU > 0
                                THEN STD.SKORIIRISU
                                ELSE USD.FUSRDEC2
                            END) / USD.FUSRDEC3
                        )
                    END AS c32
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the number of pallets, calculated based on predefined logic.

---

### c33: **Whether Movement Ticket is Issued (移動票発行有無)**

- **Header Label:** `Whether Movement Ticket is Issued (移動票発行有無)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  Whether the movement ticket is issued is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `MOVE_TICKET_ISSUED`.
- **Save Destination:** `T_HANTEI.MOVE_TICKET_ISSUED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement ticket has been issued, fetched from the `T_HANTEI` table.

---

### c34: **Completion of Movement (移動完了有無)**

- **Header Label:** `Completion of Movement (移動完了有無)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  The completion of movement is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `MOVE_FINISHED`.
- **Save Destination:** `T_HANTEI.MOVE_FINISHED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement has been completed, fetched from the `T_HANTEI` table.

---

### c35: **Multiple Locations Inventory Flag (複数拠点在庫フラグ)**

- **Header Label:** `Multiple Locations Inventory Flag (複数拠点在庫フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  The multiple locations inventory flag is calculated by counting stock entries from the relevant inventory tables (`ERP_TUNITYSTOCKHST_ALL` or `ERP_INVDTF`). A flag is set depending on the count.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the multiple locations inventory flag, calculated based on logic involving `ERP_TUNITYSTOCKHST_ALL` or `ERP_INVDTF`.

---

### c36: **Total Number of Passed Inventories (合格在庫総数)**

- **Header Label:** `Total Number of Passed Inventories (合格在庫総数)`
- **Data Type:** `Integer`
- **Custom render:** `Integer`
- **Source:**  
  The total number of passed inventories is fetched from the `V_SCREPORT` table by matching the `ITEM_ID`. It returns `PASSED_STOCK_QTY`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the total number of passed inventories, fetched from the `V_SCREPORT` table.

---

### c37: **Under Stock Days Flag (在庫日数過少フラグ)**

- **Header Label:** `Under Stock Days Flag (在庫日数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  1. If the stock days (`V_SCREPORT.STOCK_DAYS`) are less than 15 days, the flag is set to `'◯'` (indicating that stock days are below the threshold).
  
  2. If the stock days are 15 or more, the flag is set to `'X'` (indicating sufficient stock days).
   ```sql
  CASE WHEN V_SCREPORT.STOCK_DAYS < 15 THEN '◯' ELSE 'X' END AS c37
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the under stock days flag, calculated based on predefined logic.

---

### c38: **Under Shipment Flag for the Current Month (当月残出荷予定数過少フラグ)**

- **Header Label:** `Under Shipment Flag for the Current Month (当月残出荷予定数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  1. If the difference between the planned monthly quantity (`V_SCREPORT.MONTH_PLNQTY`) and the actual monthly quantity (`V_SCREPORT.MONTH_QTY`) is negative, the flag is set to `'◯'` (indicating that shipments are under the planned quantity).
  
  2. If the available passed stock quantity (`V_SCREPORT.PASSED_STOCK_QTY`) is less than the difference between the planned and actual quantities for the month, the flag is also set to `'◯'`.
  
  3. Otherwise, the flag is set to `'X'` (indicating sufficient shipments for the current month).
   ```sql
  CASE
                        WHEN (V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY) < 0 THEN '◯'
                        WHEN V_SCREPORT.PASSED_STOCK_QTY < (V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY) THEN '◯'
                        ELSE 'X'
                    END AS c38
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the under shipment flag for the current month, calculated based on predefined logic.

---

### c39: **Short-Term Under-Planned Flag for the Following Month (翌月短期予定過少フラグ)**

- **Header Label:** `Short-Term Under-Planned Flag for the Following Month (翌月短期予定過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  1. If the available passed stock quantity (`V_SCREPORT.PASSED_STOCK_QTY`) is less than the sum of the remaining planned monthly quantity (`V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY`) and the next month's planned quantity (`V_SCREPORT.NEXT_MONTH_PLNQTY`), the flag is set to `'◯'`.
  
  2. If the remaining planned quantity for the current month (`V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY`) is negative, the flag is set to `'◯'`.
  
  3. If the available passed stock quantity (`V_SCREPORT.PASSED_STOCK_QTY`) is less than the next month's planned quantity (`V_SCREPORT.NEXT_MONTH_PLNQTY`), the flag is set to `'◯'`.

  4. Otherwise, the flag is set to `'X'`, indicating that the planned shipments for the following month are sufficient.
   ```sql
  CASE
                        WHEN V_SCREPORT.PASSED_STOCK_QTY < (V_SCREPORT.MONTH_PLNQTY- MONTH_QTY + V_SCREPORT.NEXT_MONTH_PLNQTY) THEN '◯'
                        WHEN V_SCREPORT.MONTH_PLNQTY- MONTH_QTY < 0 THEN '◯'
                        WHEN  V_SCREPORT.PASSED_STOCK_QTY < V_SCREPORT.NEXT_MONTH_PLNQTY THEN '◯'
                        ELSE 'X'
                    END AS c39
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the short-term under-planned flag for the following month, calculated based on predefined logic.

---

### c40: **Judgment Report (成績書)**

- **Header Label:** `Judgment Report (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=7)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**  
  The status of the judgment report is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `CERTIFICATE_STATUS`.
- **Save Destination:** `T_HANTEI.CERTIFICATE_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the status of the judgment report, fetched from the `T_HANTEI` table.

---

### c41: **Send Email (メール送信)**

- **Header Label:** `Send Email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=8)
  - From `M_DISPLAY_ITEMS`, use VALUE as label for UI
- **Source:**  
  Whether an email has been sent is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `SEND_MAIL_STATUS`.
- **Save Destination:** `T_HANTEI.SEND_MAIL_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether an email has been sent, fetched from the `T_HANTEI` table.

---

### c42: **Date of NETP Judgment (NETP判定日)**

- **Header Label:** `Date of NETP Judgment (NETP判定日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The date of the NETP judgment is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `NETP_JUDGE_DATE`.
- **Save Destination:** `T_HANTEI.NETP_JUDGE_DATE`
- **Validation:** `If null,「未」(not yet) is displayed.`
- **Options:** `N/A`
- **Remarks:** Displays the date of the NETP judgment, fetched from the `T_HANTEI` table.

---

### c43: **Last Update (最終更新日時)**

- **Header Label:** `Last Update (最終更新日時)`
- **Data Type:** `Datetime`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The last update time is fetched from the `T_RESPONSE` table by matching the `RESPONSE_ID`. It returns `UPDATE_RECORD_TIME`.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the last update time, fetched from the `T_RESPONSE` table.

---

---------------------------------------------------------
---------------------------------------------------------


## Judgement List (Edit Mode)

### c16: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=2)
  - From `M_DISPLAY_ITEMS`, use  ID as key and VALUE as label for UI
- **Source:**  
  The urgent sign is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `URGENT_TYPE`.
- **Save Destination:** `T_HANTEI.URGENT_TYPE`
- **Validation:** `N/A`
- **Options:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=2)
  - From `M_DISPLAY_ITEMS`, use ID as the key and VALUE as the label for options
- **Remarks:** Displays the urgent sign, fetched from the `T_HANTEI` table.

---

### c17: **Urgent Request Date (急ぎ依頼日)**

- **Header Label:** `Urgent Request Date (急ぎ依頼日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The urgent request date is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns the `URGENT_REQ_DATE`.
- **Save Destination:** `T_HANTEI.URGENT_REQ_DATE`
- **Validation:** `Set today's date when setting「急ぎサイン」(c16). Required when input 「急ぎサイン」(c16).`
- **Options:** `N/A`
- **Remarks:** Displays the urgent request date, fetched from the `T_HANTEI` table.

---

### c18: **Desired Date of Urgent Judgment (急ぎ判定希望日)**

- **Header Label:** `Desired Date of Urgent Judgment (急ぎ判定希望日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The desired date for urgent judgment is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns the `URGENT_JUDGE_REQ_DATE`.
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_DATE`
- **Validation:** `When the「急ぎサイン」(c16) is other than「1=急」(1=urgent), input is not possible. Required when「急ぎサイン」(c16) is「1=急」(1=urgent).`
- **Options:** `N/A`
- **Remarks:** Displays the desired date for urgent judgment, fetched from the `T_HANTEI` table.

---

### c19: **Desired Time for Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time for Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:**  
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=4)
  - From `M_DISPLAY_ITEMS`, use  ID as key and VALUE as label for UI
- **Source:**  
  The `URGENT_JUDGE_REQ_TIME` is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns the `URGENT_JUDGE_REQ_TIME` then it will be matched with the `ID` and item from `M_DISPLAY_ITEM.
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_TIME`
- **Validation:** `When the「急ぎサイン」(c16) is other than「1=急」(1=urgent), input is not possible.`
- **Options:** 
  - Fetch items from M_DISPLAY_ITEMS (ITEM_NO=4)
  - From M_DISPLAY_ITEMS, use ID as key and VALUE as label for options
- **Remarks:** Displays the desired time for urgent judgment, fetched from the `T_HANTEI` table.

---

### c23: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**  
  The attribute (color-coded) is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns the `URGENT_ATTRIBUTE`.
- **Save Destination:** `T_HANTEI.URGENT_ATTRIBUTE`
- **Validation:** `When「急ぎサイン」(c16) is「1=急」(1=urgent), input required.`
- **Options:** `N/A`
- **Remarks:** Displays the attribute as color-coded information, fetched from the `T_HANTEI` table.

---

### c24: **Desired Movement Date (移動希望日)**

- **Header Label:** `Desired Movement Date (移動希望日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  - If the plant division name in the RSOS_V_JUDGE_PRODUCT table is '大阪' and the urgent type in the T_HANTEI table is 1, check if the plant division name or location in the T_HANTEI or RSOS_M_LOCATION tables is either '梅田倉庫' or 'トランスシティ'.
  - If the condition is met, and the response answer date (URGENT_JUDGE_RESP_ANS_DATE) in the T_RESPONSE table or the urgent judge request date (URGENT_JUDGE_REQ_DATE) in the T_HANTEI table exists, calculate the maximum date (FDATE) from the ERP_CALEM table where the date (FDATE) is greater than either the response answer date or request date, considering working days (FHOLIDAYFLG = 'W').
  - If the plant division is '上野工場' or not '大阪', no movement date is calculated.
  - If the urgent type in the T_HANTEI table is not 1, calculate based on other conditions by considering plant division name or location and response time from the T_RESPONSE table.
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '大阪' AND T_HANTEI.URGENT_TYPE = 1 THEN
                            CASE
                                WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                        ELSE
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                    END
                                ELSE
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN
                                            COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE)
                                        ELSE
                                            (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                    END
                            END
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '上野工場' OR RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME <> '大阪' THEN
                            NULL
                        ELSE
                            CASE
                                WHEN T_HANTEI.URGENT_TYPE != 1 THEN
                                    CASE
                                        WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                                ELSE
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 3) AS DATE_LIST)
                                            END
                                        ELSE
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 1) AS DATE_LIST)
                                                ELSE
                                                    (SELECT MAX(FDATE) FROM (SELECT FDATE FROM ERP_CALEM WHERE FCALETYP = 'A' AND FDATE > COALESCE(T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE,
                            T_HANTEI.URGENT_JUDGE_REQ_DATE,
                            RSOS_V_JUDGE_PRODUCT.SHIP_JUDGE_SCH_DATE) AND FHOLIDAYFLG = 'W' ORDER BY FDATE ASC LIMIT 2) AS DATE_LIST)
                                            END
                                    END
                                ELSE
                                    NULL
                            END
                    END AS MOVE_REQ_DATE
  ```
- **Save Destination:** `T_HANTEI.MOVE_REQ_DATE`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the desired movement date, calculated based on predefined logic.

---

### c25: **Evening Packing・Morning Delivery Sign (宵積サイン)**

- **Header Label:** `Evening Packing・Morning Delivery Sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(AM/PM)` 1= AM, 0=PM
- **Source:**  
   1. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '大阪' and the urgent type in the `T_HANTEI` table is 1, then:
     - Check if the plant division name or location in the `T_HANTEI` or `RSOS_M_LOCATION` tables is either '梅田倉庫' or 'トランスシティ'.
     - If the response answer date (`URGENT_JUDGE_RESP_ANS_DATE`) in the `T_RESPONSE` table or the urgent judge request date (`URGENT_JUDGE_REQ_DATE`) in the `T_HANTEI` table is present and the response answer time or request time is 1, then return 0; otherwise, return 1.
  
  2. If the plant division name in the `RSOS_V_JUDGE_PRODUCT` table is '上野工場' or any value other than '大阪', return 0.

  3. If the urgent type in the `T_HANTEI` table is not 1, similar logic is applied based on the plant division name, urgent judge request date, and response times from the `T_RESPONSE` table.

  This logic uses data from `RSOS_V_JUDGE_PRODUCT`, `T_HANTEI`, `T_RESPONSE`, and `RSOS_M_LOCATION` tables to determine if the evening packing or morning delivery sign should be flagged (0 or 1).
  ```sql
  CASE
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '大阪' AND T_HANTEI.URGENT_TYPE = 1 THEN
                            CASE
                                WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN 0 ELSE 0
                                    END
                                ELSE
                                    CASE
                                        WHEN
                                            (CASE
                                                WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                ELSE 0
                                            END) = 1 THEN 1 ELSE 0
                                    END
                            END
                        WHEN RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME = '上野工場' OR RSOS_V_JUDGE_PRODUCT.PLANT_DIVISION_NAME <> '大阪' THEN
                            0
                        ELSE
                            CASE
                                WHEN T_HANTEI.URGENT_TYPE != 1 THEN
                                    CASE
                                        WHEN COALESCE(T_HANTEI.PLANT_DIVISION_NAME, RSOS_M_LOCATION.LOCATION_NAME) IN ('梅田倉庫', 'トランスシティ') THEN
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN 0 ELSE 0
                                            END
                                        ELSE
                                            CASE
                                                WHEN
                                                    (CASE
                                                        WHEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_DATE IS NOT NULL THEN T_RESPONSE.URGENT_JUDGE_RESP_ANS_TIME
                                                        WHEN T_HANTEI.URGENT_JUDGE_REQ_DATE IS NOT NULL THEN T_HANTEI.URGENT_JUDGE_REQ_TIME
                                                        ELSE 0
                                                    END) = 1 THEN 1 ELSE 0
                                            END
                                    END
                                ELSE
                                    0
                            END
                    END AS VESPER_FLAG
  ```
- **Save Destination:** `T_HANTEI.VESPER_FLAG`
- **Validation:** `N/A`
- **Options:** `1= AM, 0=PM`
- **Remarks:** Displays the evening packing or morning delivery sign, calculated based on predefined logic.

---

### c31: **Destination/Delivery (移動先/納品先)**

- **Header Label:** `Destination/Delivery (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**  
  The destination or delivery name is determined either from the `T_HANTEI` or `RSOS_M_LOCATION` table based on whether the delivery destination is available or fetched from the inventory location.
- **Save Destination:** `T_HANTEI.DELIVERY_DESTINATION_NAME`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the destination or delivery name. If no data is found in `T_HANTEI`, it is fetched from `RSOS_M_LOCATION`.

---

### c33: **Whether Movement Ticket is Issued (移動票発行有無)**

- **Header Label:** `Whether Movement Ticket is Issued (移動票発行有無)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  Whether the movement ticket is issued is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `MOVE_TICKET_ISSUED`.
- **Save Destination:** `T_HANTEI.MOVE_TICKET_ISSUED`
- **Validation:** `N/A`
- **Options:** `0 配荷,1 生産トラブル,2 輸出引き当て,3 セット加工用単品抜き取り`
- **Remarks:** Displays whether the movement ticket has been issued, fetched from the `T_HANTEI` table.

---

### c34: **Completion of Movement (移動完了有無)**

- **Header Label:** `Completion of Movement (移動完了有無)`
- **Data Type:** `TinyInt`
- **Custom render:** `String(0=X ,1=○)`
- **Source:**  
  The completion of movement is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `MOVE_FINISHED`.
- **Save Destination:** `T_HANTEI.MOVE_FINISHED`
- **Validation:** `N/A`
- **Options:** `0 配荷,1 生産トラブル,2 輸出引き当て,3 セット加工用単品抜き取り`
- **Remarks:** Displays whether the movement has been completed, fetched from the `T_HANTEI` table.

---

### c40: **Judgment Report (成績書)**

- **Header Label:** `Judgment Report (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=7)
  - From `M_DISPLAY_ITEMS`, use ID as key and VALUE as label for UI
- **Source:**  
  The status of the judgment report is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `CERTIFICATE_STATUS`.
- **Save Destination:** `T_HANTEI.CERTIFICATE_STATUS`
- **Validation:** `N/A`
- **Options:** 
  - Fetch items from M_DISPLAY_ITEMS (ITEM_NO=7)
- From M_DISPLAY_ITEMS, use ID as key and VALUE as label for options
- **Remarks:** Displays the status of the judgment report, fetched from the `T_HANTEI` table.

---

### c41: **Send Email (メール送信)**

- **Header Label:** `Send Email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** 
  - Fetch items from `M_DISPLAY_ITEMS` (ITEM_NO=8)
  - From `M_DISPLAY_ITEMS`, use ID as key and VALUE as label for UI
- **Source:**  
  Whether an email has been sent is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns `SEND_MAIL_STATUS`.
- **Save Destination:** `T_HANTEI.SEND_MAIL_STATUS`
- **Validation:** `N/A`
- **Options:** 
  - Fetch items from M_DISPLAY_ITEMS (ITEM_NO=8)
- From M_DISPLAY_ITEMS, use ID as key and VALUE as label for options
- **Remarks:** Displays whether an email has been sent, fetched from the `T_HANTEI` table.

---

### c42: **Date of NETP Judgment (NETP判定日)**

- **Header Label:** `Date of NETP Judgment (NETP判定日)`
- **Data Type:** `Date`
- **Custom render:** `String(YYYY-MM-DD)`
- **Source:**  
  The date of the NETP judgment is fetched from the `T_HANTEI` table by matching the `ITEM_NO`. It returns the `NETP_JUDGE_DATE`.
- **Save Destination:** `T_HANTEI.NETP_JUDGE_DATE`
- **Validation:** `If null,「未」(not yet) is displayed.`
- **Options:** `N/A`
- **Remarks:** Displays the date of the NETP judgment, fetched from the `T_HANTEI` table.

---------------------------------------------------------
---------------------------------------------------------


## Search Modal

### s1-1: **Person in Charge (担当者)**

- **Header Label:** `Person in Charge (担当者)`
- **Data Type:** `String`
- **Custom render:** `String`
- **Filter column:** `c1`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.TANTO%'` (`LIKE '%判定一覧検索条件.担当者%'`)
- **Save Destination:** `cfg_kg00100_search_filters.TANTO`
- **Source:** 
   The person in charge (`TANTO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for the person in charge (`判定一覧検索条件.担当者`).
- **Remarks:** `This field allows the user to search for the person in charge.`

---

### s2-1: **In-house/Outsourcing (内製/外製)**

- **Header Label:** `In-house/Outsourcing (内製/外製)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c2`
- **search condition:** `= cfg_kg00100_search_filters.IN_OUT_SOURCING` (`= 判定一覧検索条件.内製/外製`)
- **Save Destination:** `cfg_kg00100_search_filters.IN_OUT_SOURCING`
- **Source:** 
   The in-house or outsourcing value (`IN_OUT_SOURCING`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for in-house or outsourcing (`判定一覧検索条件.内製/外製`).
- **Remarks:** `This field allows the user to search for whether the product is in-house or outsourced.`

---

### s3-1: **Item CD (基準品目CD)**

- **Header Label:** `Item CD (基準品目CD)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c3`
- **search condition:** `= cfg_kg00100_search_filters.ITEM_CODE` (`= 判定一覧検索条件.基準品目CD`)
- **Save Destination:** `cfg_kg00100_search_filters.ITEM_CODE`
- **Source:** 
   The item code (`ITEM_CODE`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for the item code (`判定一覧検索条件.基準品目CD`).
- **Remarks:** `This field allows the user to search based on the reference item code (基準品目CD).`

---

### s4-1: **Production Abbreviation (生産略称)**

- **Header Label:** `Production Abbreviation (生産略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c4`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.PRODUCT_SHORT_NAME%'` (`LIKE '%判定一覧検索条件.生産略称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.PRODUCT_SHORT_NAME`
- **Source:** 
   The production abbreviation (`PRODUCT_SHORT_NAME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for production abbreviation (`判定一覧検索条件.生産略称`).
- **Remarks:** `This field allows the user to search based on the production abbreviation (生産略称).`

---

### s5-1: **Sales Abbreviation (販売略称)**

- **Header Label:** `Sales Abbreviation (販売略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c5`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.SALES_SHORT_NAME%'` (`LIKE '%判定一覧検索条件.販売略称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.SALES_SHORT_NAME`
- **Source:** 
   The sales abbreviation (`SALES_SHORT_NAME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for sales abbreviation (`判定一覧検索条件.販売略称`).
- **Remarks:** `This field allows the user to search based on the sales abbreviation (販売略称).`

---

### s6-1: **Lot (ロット)**

- **Header Label:** `Lot (ロット)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c6`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.LOT%'` (`LIKE '%判定一覧検索条件.ロット%'`)
- **Save Destination:** `cfg_kg00100_search_filters.LOT`
- **Source:** 
   The lot (`LOT`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for lot (`判定一覧検索条件.ロット`).
- **Remarks:** `This field allows the user to search based on the lot number (ロット).`

---

### s7-1: **Delivery Date "from" (納品日from)**

- **Header Label:** `Delivery Date "from" (納品日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c7`
- **search condition:** `>= cfg_kg00100_search_filters.DELIVERY_DATE_FROM` (`>= 判定一覧検索条件.納品日from`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DATE_FROM`
- **Source:** 
   The delivery date (`DELIVERY_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for delivery date (`判定一覧検索条件.納品日from`).
- **Remarks:** `This field filters data by delivery date starting from a specific date.`

---

### s7-2: **Delivery Date "to" (納品日to)**

- **Header Label:** `Delivery Date "to" (納品日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c7`
- **search condition:** `<= cfg_kg00100_search_filters.DELIVERY_DATE_TO` (`<= 判定一覧検索条件.納品日to`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DATE_TO`
- **Source:** 
   The delivery date (`DELIVERY_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for delivery date (`判定一覧検索条件.納品日to`).
- **Remarks:** `This field filters data by delivery date up to a specific date.`

---

### s8-1: **Production Building/Outsourcing (生産棟/外製先)**

- **Header Label:** `Production Building/Outsourcing (生産棟/外製先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c8`
- **search condition:** `= cfg_kg00100_search_filters.PLANT_DIVISION_CODE` (`= 判定一覧検索条件.生産棟/外製先`)
- **Save Destination:** `cfg_kg00100_search_filters.PLANT_DIVISION_CODE`
- **Source:** 
   The production building or outsourcing value (`PLANT_DIVISION_CODE`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for production building or outsourcing (`判定一覧検索条件.生産棟/外製先`).
- **Remarks:** `This field filters data by the production building or outsourcing location.`

---

### s9-1: **Item Name (品目名称)**

- **Header Label:** `Item Name (品目名称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c9`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.ITEM_NAME%'` (`LIKE '%判定一覧検索条件.品目名称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.ITEM_NAME`
- **Source:** 
   The item name (`ITEM_NAME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for item name (`判定一覧検索条件.品目名称`).
- **Remarks:** `This field filters data by the item name using a partial match.`

---

### s10-1: **Date of Dispensing "from" (調合日from)**

- **Header Label:** `Date of Dispensing "from" (調合日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c10`
- **search condition:** `>= cfg_kg00100_search_filters.MIXTURE_DATE_FROM` (`>= 判定一覧検索条件.調合日from`)
- **Save Destination:** `cfg_kg00100_search_filters.MIXTURE_DATE_FROM`
- **Source:** 
   The dispensing date (`MIXTURE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for dispensing date (`判定一覧検索条件.調合日from`).
- **Remarks:** `This field filters the results for the dispensing date

 starting from a specified date.`

---

### s10-2: **Date of Dispensing "to" (調合日to)**

- **Header Label:** `Date of Dispensing "to" (調合日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c10`
- **search condition:** `<= cfg_kg00100_search_filters.MIXTURE_DATE_TO` (`<= 判定一覧検索条件.調合日to`)
- **Save Destination:** `cfg_kg00100_search_filters.MIXTURE_DATE_TO`
- **Source:** 
   The dispensing date (`MIXTURE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for dispensing date (`判定一覧検索条件.調合日to`).
- **Remarks:** `This field filters the results for the dispensing date up to a specified date.`

---

### s11-1: **Filling Date "from" (充填日from)**

- **Header Label:** `Filling Date "from" (充填日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c11`
- **search condition:** `>= cfg_kg00100_search_filters.FILL_DATE_FROM` (`>= 判定一覧検索条件.充填日from`)
- **Save Destination:** `cfg_kg00100_search_filters.FILL_DATE_FROM`
- **Source:** 
   The filling date (`FILL_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for filling date (`判定一覧検索条件.充填日from`).
- **Remarks:** `This field filters the results starting from the specified filling date.`

---

### s11-2: **Filling Date "to" (充填日to)**

- **Header Label:** `Filling Date "to" (充填日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c11`
- **search condition:** `<= cfg_kg00100_search_filters.FILL_DATE_TO` (`<= 判定一覧検索条件.充填日to`)
- **Save Destination:** `cfg_kg00100_search_filters.FILL_DATE_TO`
- **Source:** 
   The filling date (`FILL_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for filling date (`判定一覧検索条件.充填日to`).
- **Remarks:** `This field filters the results up to the specified filling date.`

---

### s12-1: **Packing Date "from" (包装日from)**

- **Header Label:** `Packing Date "from" (包装日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c12`
- **search condition:** `>= cfg_kg00100_search_filters.WRAP_DATE_FROM` (`>= 判定一覧検索条件.包装日from`)
- **Save Destination:** `cfg_kg00100_search_filters.WRAP_DATE_FROM`
- **Source:** 
   The packing date (`WRAP_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for packing date (`判定一覧検索条件.包装日from`).
- **Remarks:** `This field filters the results starting from the specified packing date.`

---

### s12-2: **Packing Date "to" (包装日to)**

- **Header Label:** `Packing Date "to" (包装日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c12`
- **search condition:** `<= cfg_kg00100_search_filters.WRAP_DATE_TO` (`<= 判定一覧検索条件.包装日to`)
- **Save Destination:** `cfg_kg00100_search_filters.WRAP_DATE_TO`
- **Source:** 
   The packing date (`WRAP_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for packing date (`判定一覧検索条件.包装日to`).
- **Remarks:** `This field filters the results up to the specified packing date.`

---

### s13-1: **Usual Judgment Date "from" (通常判定日from)**

- **Header Label:** `Usual Judgment Date "from" (通常判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c14`
- **search condition:** `>= cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_FROM` (`>= 判定一覧検索条件.通常判定日from`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_FROM`
- **Source:** 
   The usual judgment date (`NORMAL_JUDGE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment date (`判定一覧検索条件.通常判定日from`).
- **Remarks:** `This field filters the results from the specified usual judgment date onward.`

---

### s13-2: **Usual Judgment Date "to" (通常判定日to)**

- **Header Label:** `Usual Judgment Date "to" (通常判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c14`
- **search condition:** `<= cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_TO` (`<= 判定一覧検索条件.通常判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_TO`
- **Source:** 
   The usual judgment date (`NORMAL_JUDGE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment date (`判定一覧検索条件.通常判定日to`).
- **Remarks:** `This field filters the results up to the specified usual judgment date.`

---

### s14-1: **Test Status (試験ステータス)**

- **Header Label:** `Test Status (試験ステータス)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c15`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.INSPECTION_STATUS%'` (`LIKE '%判定一覧検索条件.試験ステータス%'`)
- **Save Destination:** `cfg_kg00100_search_filters.INSPECTION_STATUS`
- **Source:** 
   The test status (`INSPECTION_STATUS`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for test status (`判定一覧検索条件.試験ステータス`).
- **Remarks:** `Filters the data based on the inspection status, allowing for partial matches.`

---

### s15-1: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c16`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_TYPE` (`= 判定一覧検索条件.急ぎサイン`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_TYPE`
- **Source:** 
   The urgent sign (`URGENT_TYPE`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for urgent sign (`判定一覧検索条件.急ぎサイン`).
- **Remarks:** `Filters the data based on the urgent sign type, using an exact match.`

---

### s16-1: **Urgent Request Date "from" (急ぎ依頼日from)**

- **Header Label:** `Urgent Request Date "from" (急ぎ依頼日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c17`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_REQ_DATE_FROM` (`>= 判定一覧検索条件.急ぎ依頼日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_REQ_DATE_FROM`
- **Source:** 
   The urgent request date (`URGENT_REQ_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for urgent request date (`判定一覧検索条件.急ぎ依頼日from`).
- **Remarks:** `Filters the data by selecting records where the urgent request date is greater than or equal to the specified start date.`

---

### s16-2: **Urgent Request Date "to" (急ぎ依頼日to)**

- **Header Label:** `Urgent Request Date "to" (急ぎ依頼日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c17`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_REQ_DATE_TO` (`<= 判定一覧検索条件.急ぎ依頼日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_REQ_DATE_TO`
- **Source:** 
   The urgent request date (`URGENT_REQ_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for urgent request date (`判定一覧検索

条件.急ぎ依頼日to`).
- **Remarks:** `Filters the data by selecting records where the urgent request date is less than or equal to the specified end date.`

---

### s17-1: **Desired Date of Urgent Judgment "from" (急ぎ判定希望日from)**

- **Header Label:** `Desired Date of Urgent Judgment "from" (急ぎ判定希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c18`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_FROM` (`>= 判定一覧検索条件.急ぎ判定希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_FROM`
- **Source:** 
   The desired date of urgent judgment (`URGENT_JUDGE_REQ_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment date (`判定一覧検索条件.急ぎ判定希望日from`).
- **Remarks:** `Filters the data by selecting records where the desired date of urgent judgment is greater than or equal to the specified start date.`

---

### s17-2: **Desired Date of Urgent Judgment "to" (急ぎ判定希望日to)**

- **Header Label:** `Desired Date of Urgent Judgment "to" (急ぎ判定希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c18`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_TO` (`<= 判定一覧検索条件.急ぎ判定希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_TO`
- **Source:** 
   The desired date of urgent judgment (`URGENT_JUDGE_REQ_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment date (`判定一覧検索条件.急ぎ判定希望日to`).
- **Remarks:** `Filters the data by selecting records where the desired date of urgent judgment is less than or equal to the specified end date.`

---

### s18-1: **Desired Time of Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time of Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c19`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_TIME` (`= 判定一覧検索条件.急ぎ判定希望時間`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_TIME`
- **Source:** 
   The desired time of urgent judgment (`URGENT_JUDGE_REQ_TIME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment time (`判定一覧検索条件.急ぎ判定希望時間`).
- **Remarks:** `Filters the data based on the exact desired time for urgent judgment.`

---

### s19-1: **Quality Department Reply (品質部門の返信)**

- **Header Label:** `Quality Department Reply (品質部門の返信)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c20`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_RESP` (`= 判定一覧検索条件.品質部門の返信`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP`
- **Source:** 
   The quality department reply (`URGENT_JUDGE_RESP`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for department reply (`判定一覧検索条件.品質部門の返信`).
- **Remarks:** `Filters data based on the response from the quality department.`

---

### s20-1: **Corrected Judgment Date From (修正判定日from)**

- **Header Label:** `Corrected Judgment Date From (修正判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c21`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_FROM` (`>= 判定一覧検索条件.修正判定日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_FROM`
- **Source:** 
   The corrected judgment date (`URGENT_JUDGE_RESP_ANS_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for corrected judgment date (`判定一覧検索条件.修正判定日from`).
- **Remarks:** `Filters data to show results from the corrected judgment date onward.`

---

### s20-2: **Corrected Judgment Date To (修正判定日to)**

- **Header Label:** `Corrected Judgment Date To (修正判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c21`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_TO` (`<= 判定一覧検索条件.修正判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_TO`
- **Source:** 
   The corrected judgment date (`URGENT_JUDGE_RESP_ANS_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for corrected judgment date (`判定一覧検索条件.修正判定日to`).
- **Remarks:** `Filters data to show results up to the corrected judgment date.`

---

### s21-1: **Correct Judgment Time (修正判定時間)**

- **Header Label:** `Correct Judgment Time (修正判定時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c21`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_TIME` (`= 判定一覧検索条件.修正判定時間`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_TIME`
- **Source:** 
   The corrected judgment time (`URGENT_JUDGE_RESP_ANS_TIME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for judgment time (`判定一覧検索条件.修正判定時間`).
- **Remarks:** `Filters data based on the exact corrected judgment time.`

---

### s22-1: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c23`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_ATTRIBUTE` (`= 判定一覧検索条件.属性（色分け）`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_ATTRIBUTE`
- **Source:** 
   The color-coded attributes (`URGENT_ATTRIBUTE`) are fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for attributes (`判定一覧検索条件.属性（色分け）`).
- **Remarks:** `Filters data based on the color-coded attributes.`

---

### s23-1: **Moving Hope Day from (移動希望日from)**

- **Header Label:** `Moving Hope Day from (移動希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c24`
- **search condition:** `>= cfg_kg00100_search_filters.MOVE_REQ_DATE_FROM` (`>= 判定一覧検索条件.移動希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_REQ_DATE_FROM`
- **Source:** 
   The move request date (`MOVE_REQ_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for move request date (`判定一覧検索条件.移動希望日from`).
- **Remarks:** `Filters data by selecting records with a move request date starting from the specified date.`

---

### s23-2: **Moving Hope Day to (移動希望日to)**

- **Header Label:** `Moving Hope Day to (移動希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c24`
- **search condition:** `<= cfg_kg00100_search_filters.MOVE_REQ_DATE_TO` (`<= 判定一覧検索条件.移動希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_REQ_DATE_TO`
- **Source:** 
   The move request date (`MOVE_REQ_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for move request date (`判定一覧検索条件.移動希望日to`).
- **Remarks:** `Filters

 data by selecting records with a move request date up to the specified date.`

---

### s24-1: **Yoizumi sign (宵積サイン)**

- **Header Label:** `Yoizumi sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c25`
- **search condition:** `= cfg_kg00100_search_filters.VESPER_FLAG` (`= 判定一覧検索条件.宵積サイン`)
- **Save Destination:** `cfg_kg00100_search_filters.VESPER_FLAG`
- **Source:** 
   The Yoizumi sign (`VESPER_FLAG`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for Yoizumi (`判定一覧検索条件.宵積サイン`).
- **Remarks:** `Filters data based on whether the Yoizumi (evening packing) sign is flagged or not.`

---

### s25-1: **Usually the possible date of delivery is from (通常出荷可能日from)**

- **Header Label:** `Usually the possible date of delivery is from (通常出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c26`
- **search condition:** `>= cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.通常出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_FROM`
- **Source:** 
   The usual available date for shipment (`NORMAL_SHIP_POSSIBLE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for available date (`判定一覧検索条件.通常出荷可能日from`).
- **Remarks:** `Filters records where the usual available date for shipment is greater than or equal to the specified date.`

---

### s25-2: **Normal shipping date to (通常出荷可能日to)**

- **Header Label:** `Normal shipping date to (通常出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c26`
- **search condition:** `<= cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.通常出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_TO`
- **Source:** 
   The usual available date for shipment (`NORMAL_SHIP_POSSIBLE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for available date (`判定一覧検索条件.通常出荷可能日to`).
- **Remarks:** `Filters records where the usual available date for shipment is less than or equal to the specified date.`

---

### s26-1: **Expedited shipping date from (急ぎ出荷可能日from)**

- **Header Label:** `Expedited shipping date from (急ぎ出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c27`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.急ぎ出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_FROM`
- **Source:** 
   The expedited shipping date (`URGENT_SHIP_POSSIBLE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for shipping date (`判定一覧検索条件.急ぎ出荷可能日from`).
- **Remarks:** `Filters records where the expedited shipping date is greater than or equal to the specified date.`

---

### s26-2: **Expedited shipping date to (急ぎ出荷可能日to)**

- **Header Label:** `Expedited shipping date to (急ぎ出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c27`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.急ぎ出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_TO`
- **Source:** 
   The expedited shipping date (`URGENT_SHIP_POSSIBLE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for shipping date (`判定一覧検索条件.急ぎ出荷可能日to`).
- **Remarks:** `Filters records where the expedited shipping date is less than or equal to the specified date.`

---

### s27-1: **Relaxed shipping date from (緩め出荷可能日from)**

- **Header Label:** `Relaxed shipping date from (緩め出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c28`
- **search condition:** `>= cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.緩め出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_FROM`
- **Source:** 
   The relaxed shipping date (`LATE_SHIP_POSSIBLE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for relaxed shipping date (`判定一覧検索条件.緩め出荷可能日from`).
- **Remarks:** `Filters records where the relaxed shipping date is greater than or equal to the specified date.`

---

### s27-2: **Relaxed shipping date to (緩め出荷可能日to)**

- **Header Label:** `Relaxed shipping date to (緩め出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c28`
- **search condition:** `<= cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.緩め出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_TO`
- **Source:** 
   The relaxed shipping date (`LATE_SHIP_POSSIBLE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for relaxed shipping date (`判定一覧検索条件.緩め出荷可能日to`).
- **Remarks:** `Filters records where the relaxed shipping date is less than or equal to the specified date.`

---

### s28-1: **Desired date for loosening judgment from (緩め判定希望日from)**

- **Header Label:** `Desired date for loosening judgment from (緩め判定希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c29`
- **search condition:** `>= cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_FROM` (`>= 判定一覧検索条件.緩め判定希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_FROM`
- **Source:** 
   The desired date for loosening judgment (`LATE_SHIP_JUDGE_REQ_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for loosening judgment (`判定一覧検索条件.緩め判定希望日from`).
- **Remarks:** `Filters records where the desired date for loosening judgment is greater than or equal to the specified date.`

---

### s28-2: **Desired date for loosening judgment to (緩め判定希望日to)**

- **Header Label:** `Desired date for loosening judgment to (緩め判定希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c29`
- **search condition:** `<= cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_TO` (`<= 判定一覧検索条件.緩め判定希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_TO`
- **Source:** 
   The desired date for loosening judgment (`LATE_SHIP_JUDGE_REQ_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for loosening judgment (`判定一覧検索条件.緩め判定希望日to`).
- **Remarks:** `Filters records where the desired date for loosening judgment is less than or equal to the specified date.`

---

### s29-1: **Desired loosening judgment time (緩め判定希望時間)**

- **Header Label:** `Desired loosening judgment time (緩め判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c30`
- **search condition:** `= cfg_kg00100_search_filters.L

ATE_SHIP_JUDGE_REQ_TIME` (`= 判定一覧検索条件.緩め判定希望時間`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_TIME`
- **Source:** 
   The desired time for loosening judgment (`LATE_SHIP_JUDGE_REQ_TIME`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for loosening judgment time (`判定一覧検索条件.緩め判定希望時間`).
- **Remarks:** `Filters records by the exact desired loosening judgment time.`

---

### s30-1: **Moving destination/delivery destination (移動先/納品先)**

- **Header Label:** `Moving destination/delivery destination (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c31`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.DELIVERY_DESTINATION%'` (`LIKE '%判定一覧検索条件.移動先/納品先%'`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DESTINATION`
- **Source:** 
   The delivery destination (`DELIVERY_DESTINATION`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for delivery destination (`判定一覧検索条件.移動先/納品先`).
- **Remarks:** `Filters records by matching the moving or delivery destination.`

---

### s31-1: **Issuance of transfer ticket? (移動票発行有無)**

- **Header Label:** `Issuance of transfer ticket? (移動票発行有無)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c33`
- **search condition:** `= cfg_kg00100_search_filters.MOVE_TICKET_ISSUED` (`= 判定一覧検索条件.移動票発行有無`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_TICKET_ISSUED`
- **Source:** 
   The transfer ticket issuance status (`MOVE_TICKET_ISSUED`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for transfer ticket issuance (`判定一覧検索条件.移動票発行有無`).
- **Remarks:** `Filters records based on whether the transfer ticket has been issued.`

---

### s32-1: **Is the move complete? (移動完了有無)**

- **Header Label:** `Is the move complete? (移動完了有無)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c34`
- **search condition:** `= cfg_kg00100_search_filters.MOVE_FINISHED` (`= 判定一覧検索条件.移動完了有無`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_FINISHED`
- **Source:** 
   The move completion status (`MOVE_FINISHED`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for move completion (`判定一覧検索条件.移動完了有無`).
- **Remarks:** `Filters records based on whether the movement has been completed.`

---

### s33-1: **Multi-location inventory flag (複数拠点在庫フラグ)**

- **Header Label:** `Multi-location inventory flag (複数拠点在庫フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c35`
- **search condition:** `= cfg_kg00100_search_filters.MULTIPLE_PLANT_INV_STATUS` (`= 判定一覧検索条件.複数拠点在庫フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.MULTIPLE_PLANT_INV_STATUS`
- **Source:** 
   The multi-location inventory flag (`MULTIPLE_PLANT_INV_STATUS`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for multi-location inventory (`判定一覧検索条件.複数拠点在庫フラグ`).
- **Remarks:** `Filters records based on the multi-location inventory flag status.`

---

### s34-1: **Insufficient inventory days flag (在庫日数過少フラグ)**

- **Header Label:** `Insufficient inventory days flag (在庫日数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c37`
- **search condition:** `= cfg_kg00100_search_filters.INV_DAYS_SHORT` (`= 判定一覧検索条件.在庫日数過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.INV_DAYS_SHORT`
- **Source:** 
   The insufficient inventory days flag (`INV_DAYS_SHORT`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for inventory days (`判定一覧検索条件.在庫日数過少フラグ`).
- **Remarks:** `Filters records based on the insufficient inventory days flag.`

---

### s35-1: **Insufficient number of scheduled shipments remaining for this month flag (当月残出荷予定数過少フラグ)**

- **Header Label:** `Insufficient number of scheduled shipments remaining for this month flag (当月残出荷予定数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c38`
- **search condition:** `= cfg_kg00100_search_filters.CURRENT_MONTH_PLAN_SHORT` (`= 判定一覧検索条件.当月残出荷予定数過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.CURRENT_MONTH_PLAN_SHORT`
- **Source:** 
   The current month plan shortfall flag (`CURRENT_MONTH_PLAN_SHORT`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for current month plan (`判定一覧検索条件.当月残出荷予定数過少フラグ`).
- **Remarks:** `Filters records based on the insufficient number of scheduled shipments remaining for this month.`

---

### s36-1: **Short-term underscheduled flag for next month (翌月短期予定過少フラグ)**

- **Header Label:** `Short-term underscheduled flag for next month (翌月短期予定過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c39`
- **search condition:** `= cfg_kg00100_search_filters.NEXT_MONTH_PLAN_SHORT` (`= 判定一覧検索条件.翌月短期予定過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.NEXT_MONTH_PLAN_SHORT`
- **Source:** 
   The next month plan shortfall flag (`NEXT_MONTH_PLAN_SHORT`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for next month plan (`判定一覧検索条件.翌月短期予定過少フラグ`).
- **Remarks:** `Filters records based on the short-term underscheduled flag for the following month.`

---

### s37-1: **Report card (成績書)**

- **Header Label:** `Report card (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c40`
- **search condition:** `= cfg_kg00100_search_filters.CERTIFICATE_STATUS` (`= 判定一覧検索条件.成績書`)
- **Save Destination:** `cfg_kg00100_search_filters.CERTIFICATE_STATUS`
- **Source:** 
   The report card status (`CERTIFICATE_STATUS`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for report card (`判定一覧検索条件.成績書`).
- **Remarks:** `Filters records based on the report card status.`

---

### s38-1: **Send email (メール送信)**

- **Header Label:** `Send email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c41`
- **search condition:** `= cfg_kg00100_search_filters.SEND_MAIL_STATUS` (`= 判定一覧検索条件.メール送信`)
- **Save Destination:** `cfg_kg00100_search_filters.SEND_MAIL_STATUS`
- **Source:** 
   The email send status (`SEND_MAIL_STATUS`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for email status (`判定一覧検索条件.メール送信`).
- **Remarks:** `Filters records based on the email send status.`

---

### s39-1: **NETP decision date from (NETP判定日from)**

- **Header Label:** `NETP decision date from (NETP判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c42`
- **search condition:** `>= cfg_kg00100_search_filters.NETP_JUDGE_DATE_FROM` (`>= 判定一覧検索条件.NETP判定日from`)
- **Save Destination:** `cfg

_kg00100_search_filters.NETP_JUDGE_DATE_FROM`
- **Source:** 
   The NETP decision date (`NETP_JUDGE_DATE_FROM`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for NETP judgment date (`判定一覧検索条件.NETP判定日from`).
- **Remarks:** `Filters records based on the NETP decision date starting from the specified value.`

---

### s39-2: **NETP judgment date to (NETP判定日to)**

- **Header Label:** `NETP judgment date to (NETP判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c43`
- **search condition:** `<= cfg_kg00100_search_filters.NETP_JUDGE_DATE_TO` (`<= 判定一覧検索条件.NETP判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NETP_JUDGE_DATE_TO`
- **Source:** 
   The NETP judgment date (`NETP_JUDGE_DATE_TO`) is fetched from the `cfg_kg00100_search_filters` table where it matches the search condition for NETP judgment date (`判定一覧検索条件.NETP判定日to`).
- **Remarks:** `Filters records based on the NETP judgment date ending with the specified value.`

---
































