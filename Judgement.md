
## Judgement List (View Mode)

### c1: **Person in Charge (担当者)**

- **Header Label:** `Person in Charge (担当者)`
- **Data Type:** `String`
- **Custom render:** `String`
- **Source:**
  ```sql
  SELECT employee_name FROM T_HANTEI or RSOS_T_PRODUCT_ORDER WHERE employee_id:employee_id;
  ```
- **Logic:** The employee name is retrieved based on the employee_id from either the T_HANTEI or RSOS_T_PRODUCT_ORDER table. If the employee_id matches a record in either table in the given order, the corresponding employee_name is returned
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the name of the person in charge, retrieved from the T_HANTEI or RSOS_T_PRODUCT_ORDER table.

---

### c2: **In-house/Outsourcing (内製/外製)**

- **Header Label:** `In-house/Outsourcing (内製/外製)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Source:**
  ```sql
  SELECT VALUE from M_DISPLAY_ITEM join T_HANTEI by ITEM_NO;
  ```
- **Logic:** The in-house or outsourcing text value is selected from the M_DISPLAY_ITEM table. T_HANTEI table contains ITEM_NO, This ITEM_NO is available inside M_DISPLAY_ITEM table. By matching result with ITEM_NO  displays item that corresponds to either in-house or outsourcing, with the options defined as 0: 内製 (in-house) and 1: 外製 (outsourcing).
- **Save Destination:** `N/A` (Not editable)
- **Validation:** show only text value from M_DISPLAY_ITEM table which is matched with T_HANTEI.ITEM_NO and M_DISPLAY_ITEM.ITEM_NO
- **Options:** `0: 内製, 1: 外製`
- **Remarks:** Displays whether the product is in-house or outsourced. Value is fixed at 0 for in-house.

---

### c3: **Reference Item CD (基準品目CD)**

- **Header Label:** `Reference Item CD (基準品目CD)`
- **Data Type:** `Varchar`
- **Custom render:** The reference item code is retrieved from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The ITEM_CODE is returned as the reference item CD.
- **Source:**
  ```sql
  SELECT ITEM_CODE FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the reference item code, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c4: **Production Abbreviation (生産略称)**

- **Header Label:** `Production Abbreviation (生産略称)`
- **Data Type:** `Varchar`
- **Custom render:** The production abbreviation is retrieved from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The PRODUCT_SHORT_NAME is returned as the production abbreviation.
- **Source:**
  ```sql
  SELECT PRODUCT_SHORT_NAME FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the production abbreviation, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c5: **Sales Abbreviation (販売略称)**

- **Header Label:** `Sales Abbreviation (販売略称)`
- **Data Type:** `Varchar`
- **Custom render:** The sales abbreviation is retrieved from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The SALES_SHORT_NAME is returned as the sales abbreviation.
- **Source:**
  ```sql
  SELECT SALES_SHORT_NAME FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the sales abbreviation, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c6: **Lot (ロット)**

- **Header Label:** `Lot (ロット)`
- **Data Type:** `Varchar`
- **Custom render:** The lot number is fetched from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The LOT_NO is returned as the lot number.
- **Source:**
  ```sql
  SELECT LOT_NO FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the lot number, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c7: **Delivery Date (納品日)**

- **Header Label:** `Delivery Date (納品日)`
- **Data Type:** `Date`
- **Custom render:** The delivery date is fetched from the RSOS_T_PRODUCT_ORDER table by matching the ORDER_ID. The DELIVERY_DATE is returned as the delivery date.
- **Source:**
  ```sql
  SELECT DELIVERY_DATE FROM RSOS_T_PRODUCT_ORDER WHERE ORDER_ID = :order_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the delivery date, fetched from the RSOS_T_PRODUCT_ORDER table.

---

### c8: **Production Building/Outsourcing (生産棟/外製先)**

- **Header Label:** `Production Building/Outsourcing (生産棟/外製先)`
- **Data Type:** `Varchar`
- **Custom render:** The production building or outsourcing location is retrieved from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The PRODUCT_PLACE_NAME is returned as the location.
- **Source:**
  ```sql
  SELECT PRODUCT_PLACE_NAME FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the name of the production building or outsourcing location, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c9: **Item Name (品目名称)**

- **Header Label:** `Item Name (品目名称)`
- **Data Type:** `Varchar`
- **Custom render:** The item name is fetched from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The ITEM_NAME is returned as the item name.
- **Source:**
  ```sql
  SELECT ITEM_NAME FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the item name, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c10: **Date of Dispensing (調合日)**

- **Header Label:** `Date of Dispensing (調合日)`
- **Data Type:** `Date`
- **Custom render:** The date of dispensing is acquired through recursive processing based on the item’s order code and process type. It considers the maximum END_DATE or END_SCH_DATE where the process type is '1'.
- **Source:**
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
- **Custom render:** The filling date is acquired through recursive processing based on the item’s order code and process type. It considers the maximum END_DATE or END_SCH_DATE where the process type is '2'.
- **Source:**
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
- **Custom render:** The packing date is acquired through recursive processing based on the item’s order code and process type. It considers the maximum END_DATE or END_SCH_DATE where the process type is '3'.
- **Source:**
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
- **Custom render:** The planned quantity is fetched from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. Depending on whether the RECORD_QTY and END_DATE are valid, it returns RECORD_QTY or QTY.
- **Source:**
  ```sql
  SELECT QTY, RECORD_QTY FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the planned quantity. If RSOS_V_JUDGE_PRODUCT.END_DATE and RECORD_QTY are valid, RECORD_QTY is shown; otherwise, QTY is displayed.

---

### c14: **Usual Judgment Day (通常判定日)**

- **Header Label:** `Usual Judgment Day (通常判定日)`
- **Data Type:** `Date`
- **Custom render:** The usual judgment day is retrieved from the RSOS_V_JUDGE_PRODUCT table by matching the ITEM_ID. The SHIP_JUDGE_SCH_DATE is returned as the judgment day.
- **Source:**
  ```sql
  SELECT SHIP_JUDGE_SCH_DATE FROM RSOS_V_JUDGE_PRODUCT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the usual judgment day, fetched from the RSOS_V_JUDGE_PRODUCT table.

---

### c15: **Test Status (試験ステータス)**

- **Header Label:** `Test Status (試験ステータス)`
- **Data Type:** `Varchar`
- **Custom render:** The test status is fetched from the RSOS_T_PRODUCT_ORDER table by matching the ORDER_ID. The QC_STATUS is returned as the test status.
- **Source:**
  ```sql
  SELECT QC_STATUS FROM RSOS_T_PRODUCT_ORDER WHERE ORDER_ID = :order_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `Display acquired values (codes) as they are`
- **Options:** `N/A`
- **Remarks:** Displays the test status, fetched from the RSOS_T_PRODUCT_ORDER table.

---

### c16: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** The urgent sign is retrieved from the T_HANTEI table by matching the JUDGE_ID. The URGENT_TYPE is returned as the urgent sign.
- **Source:**
  ```sql
  SELECT URGENT_TYPE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_TYPE`
- **Validation:** `Input required when急ぎ依頼日(the date of urgent request), 急ぎ判定希望日(desired date of urgent Judgment)・希望時間(desired time for urgent Judgment)are input.`
- **Options:** `N/A`
- **Remarks:** Displays the urgent sign, fetched from the T_HANTEI table.

---

### c17: **Urgent Request Date (急ぎ依頼日)**

- **Header Label:** `Urgent Request Date (急ぎ依頼日)`
- **Data Type:** `Date`
- **Custom render:** The urgent request date is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_REQ_DATE is returned as the urgent request date.
- **Source:**
  ```sql
  SELECT URGENT_REQ_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_REQ_DATE`
- **Validation:** `Set today's date when setting「急ぎサイン」(c16) . Required when input 「急ぎサイン」(c16)`
- **Options:** `N/A`
- **Remarks:** Displays the urgent request date, fetched from the T_HANTEI table.

---

### c18: **Desired Date of Urgent Judgment (急ぎ判定希望日)**

- **Header Label:** `Desired Date of Urgent Judgment (急ぎ判定希望日)`
- **Data Type:** `Date`
- **Custom render:** The desired date for urgent judgment is retrieved from the T_HANTEI table by matching the JUDGE_ID. The URGENT_JUDGE_REQ_DATE is returned as the desired judgment date.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_DATE`
- **Validation:** `When the「急ぎサイン」(c16) is other than 「1=急」(1=urgent),input is not possible. And input required when「急ぎサイン」(c16) is 「1=急」(1=urgent).`
- **Options:** `N/A`
- **Remarks:** Displays the desired date for the urgent judgment, fetched from the T_HANTEI table.

---

### c19: **Desired Time for Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time for Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** The desired time for urgent judgment is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_JUDGE_REQ_TIME is returned as the desired time for judgment.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_TIME FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_TIME`
- **Validation:** `When the「急ぎサイン」(c16) is other than 「1=急」(1=urgent),input is not possible.`
- **Options:** `N/A`
- **Remarks:** Displays the desired time for the urgent judgment, fetched from the T_HANTEI table.

---

### c20: **Reply of Quality Department (品質部門の返信)**

- **Header Label:** `Reply of Quality Department (品質部門の返信)`
- **Data Type:** `TinyInt`
- **Custom render:** The reply from the quality department is fetched from the T_RESPONSE table by matching the RESPONSE_ID. The URGENT_JUDGE_RESP is returned as the reply.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP FROM T_RESPONSE WHERE RESPONSE_ID = :response_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the reply from the quality department, fetched from the T_RESPONSE table.

---

### c21: **Revision Judgment Date (修正判定日)**

- **Header Label:** `Revision Judgment Date (修正判定日)`
- **Data Type:** `Date`
- **Custom render:** The revision judgment date is fetched from the T_RESPONSE table by matching the RESPONSE_ID. The URGENT_JUDGE_RESP_ANS_DATE is returned as the revision judgment date.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP_ANS_DATE FROM T_RESPONSE WHERE RESPONSE_ID = :response_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When 修正判定時間(for c21)=1, display c21 + " AM". other than that, display c21.`
- **Options:** `N/A`
- **Remarks:** Displays the revision judgment date, fetched from the T_RESPONSE table.

---

### c22: **Revision Judgment Time (修正判定時間)**

- **Header Label:** `Revision Judgment Time (修正判定時間)`
- **Data Type:** `TinyInt`
- **Custom render:** The revision judgment time is retrieved from the T_RESPONSE table by matching the RESPONSE_ID. The URGENT_JUDGE_RESP_ANS_TIME is returned as the revision judgment time.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP_ANS_TIME FROM T_RESPONSE WHERE RESPONSE_ID = :response_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the revision judgment time, fetched from the T_RESPONSE table.

---

### c23: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** The attribute (color-coded) is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_ATTRIBUTE is returned as the attribute.
- **Source:**
  ```sql
  SELECT URGENT_ATTRIBUTE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_ATTRIBUTE`
- **Validation:** `When 「急ぎサイン」(c16) is 「1=急」 (1=urgent), input required.`
- **Options:** `N/A`
- **Remarks:** Displays the attribute as color-coded information, fetched from the T_HANTEI table.

---

### c24: **Desired Movement Date (移動希望日)**

- **Header Label:** `Desired Movement Date (移動希望日)`
- **Data Type:** `Date`
- **Custom render:** `Date`
- **Source:**
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
- **Logic:** The desired movement date is calculated using logic based on the plant division name, urgent type, and other factors. It uses the calendar (ERP_CALEM) and the maximum date after considering the relevant conditions.
- **Save Destination:** `T_HANTEI.MOVE_REQ_DATE`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the desired movement date, calculated based on predefined logic.

---

### c25: **Evening Packing・Morning Delivery Sign (宵積サイン)**

- **Header Label:** `Evening Packing・Morning Delivery Sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
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
- **Logic:** The evening packing or morning delivery sign is calculated based on the plant division name and urgent type. It considers various factors, including response times and plant locations, and returns either a 0 or 1.
- **Save Destination:** `T_HANTEI.VESPER_FLAG`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the evening packing or morning delivery sign, calculated based on predefined logic.

---

### c26: **Usual Available Date for Shipment (通常出荷可能日)**

- **Header Label:** `Usual Available Date for Shipment (通常出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** `Date`
- **Source:**
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
- **Logic:** The usual available date for shipment is calculated based on the plant division and calendar (ERP_CALEM). The logic returns the maximum available date after considering the conditions for shipment.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the usual available date for shipment, calculated based on predefined logic.
  
---

### c27: **Available Date for Express Shipment (急ぎ出荷可能日)**

- **Header Label:** `Available Date for Express Shipment (急ぎ出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** `Date`
- **Source:**
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
- **Logic:** The available date for express shipment is calculated based on the plant division and response times. It uses the calendar (ERP_CALEM) to determine the maximum date considering urgency and shipment conditions.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the available date for express shipment, calculated based on predefined logic.

---

### c28: **Available Date for Loose Shipment (緩め出荷可能日)**

- **Header Label:** `Available Date for Loose Shipment (緩め出荷可能日)`
- **Data Type:** `Date`
- **Custom render:** The available date for loose shipment is fetched from the T_NONURGENT_SHIPMENT table by matching the SHIPMENT_ID. The LATE_SHIP_POSSIBLE_DATE is returned as the loose shipment date.
- **Source:**
  ```sql
  SELECT LATE_SHIP_POSSIBLE_DATE FROM T_NONURGENT_SHIPMENT WHERE SHIPMENT_ID:shipment_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the available date for loose shipment, fetched from the T_NONURGENT_SHIPMENT table.

---

### c29: **Desired Date of Loose Judgment (緩め判定希望日)**

- **Header Label:** `Desired Date of Loose Judgment (緩め判定希望日)`
- **Data Type:** `Date`
- **Custom render:** `Date`
- **Source:**
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
- **Logic:** The desired date of loose judgment is calculated based on the T_NONURGENT_SHIPMENT and the plant division. It uses the calendar (ERP_CALEM) to determine the maximum date before the late ship possible date.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When the「急ぎサイン」(c16) is other than 「2=緩」(2=loose), input is not possible. Input required when 「急ぎサイン」(c16) is「2=緩」(2=loose)`
- **Options:** `N/A`
- **Remarks:** Displays the desired date of loose judgment, fetched from the T_NONURGENT_SHIPMENT table.

---

### c30: **Desired Time of Loose Judgment (緩め判定希望時間)**

- **Header Label:** `Desired Time of Loose Judgment (緩め判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
  ```sql
  CASE
                        WHEN T_NONURGENT_SHIPMENT.LATE_SHIP_POSSIBLE_DATE IS NULL THEN 0
                        ELSE 0
                    END AS c30
  ```
- **Logic:** The desired time of loose judgment is calculated based on whether the late ship possible date exists. If it does, a 0 is returned.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `When the「急ぎサイン」(c16) is other than 「2=緩」(2=loose), input is not possible.`
- **Options:** `N/A`
- **Remarks:** Displays the desired time of loose judgment, fetched from the T_NONURGENT_SHIPMENT table.

---

### c31: **Destination/Delivery (移動先/納品先)**

- **Header Label:** `Destination/Delivery (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
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
- **Logic:** The destination or delivery name is determined either from the T_HANTEI or RSOS_M_LOCATION table based on whether the delivery destination is available or fetched from the inventory location.
- **Save Destination:** `T_HANTEI.DELIVERY_DESTINATION_NAME`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the destination or delivery name. If no data in T_HANTEI, it is fetched from RSOS_M_LOCATION.

---

### c32: **Number of Pallets (パレット数)**

- **Header Label:** `Number of Pallets (パレット数)`
- **Data Type:** `Integer`
- **Custom render:** `Integer`
- **Source:**
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
- **Logic:** The number of pallets is calculated based on the quantity (RSOS_V_JUDGE_PRODUCT.QTY) and the pallet size (USD.FUSRDEC2) and other stock details. The result is returned after ceiling division.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the number of pallets, calculated based on predefined logic.

---

### c33: **Whether Movement Ticket is Issued (移動票発行有無)**

- **Header Label:** `Whether Movement Ticket is Issued (移動票発行有無)`
- **Data Type:** `Date`
- **Custom render:** Whether the movement ticket is issued is fetched from the T_HANTEI table by matching the JUDGE_ID. The MOVE_TICKET_ISSUED is returned as the result.
- **Source:**
  ```sql
  SELECT MOVE_TICKET_ISSUED FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.MOVE_TICKET_ISSUED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement ticket has been issued, fetched from the T_HANTEI table.

---

### c34: **Completion of Movement (移動完了有無)**

- **Header Label:** `Completion of Movement (移動完了有無)`
- **Data Type:** `Date`
- **Custom render:** The completion of movement is fetched from the T_HANTEI table by matching the JUDGE_ID. The MOVE_FINISHED is returned as the result.
- **Source:**
  ```sql
  SELECT MOVE_FINISHED FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.MOVE_FINISHED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement has been completed, fetched from the T_HANTEI table.

---

### c35: **Multiple Locations Inventory Flag (複数拠点在庫フラグ)**

- **Header Label:** `Multiple Locations Inventory Flag (複数拠点在庫フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
  ```sql
  CASE
                        WHEN ZAIKO.CNT > 1 THEN '○'
                        ELSE 'X'
                    END AS c35
  ```
- **Logic:** The multiple locations inventory flag is calculated by counting stock entries from the relevant inventory tables (ERP_TUNITYSTOCKHST_ALL or ERP_INVDTF). A flag is set depending on the count.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the multiple locations inventory flag, calculated based on logic involving ERP_TUNITYSTOCKHST_ALL or ERP_INVDTF.

---

### c36: **Total Number of Passed Inventories (合格在庫総数)**

- **Header Label:** `Total Number of Passed Inventories (合格在庫総数)`
- **Data Type:** `Integer`
- **Custom render:** The total number of passed inventories is fetched from the V_SCREPORT table by matching the ITEM_ID. The PASSED_STOCK_QTY is returned as the result.
- **Source:**
  ```sql
  SELECT PASSED_STOCK_QTY FROM V_SCREPORT WHERE ITEM_ID = :item_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the total number of passed inventories, fetched from the V_SCREPORT table.

---

### c37: **Under Stock Days Flag (在庫日数過少フラグ)**

- **Header Label:** `Under Stock Days Flag (在庫日数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
  ```sql
  CASE WHEN V_SCREPORT.STOCK_DAYS < 15 THEN '◯' ELSE 'X' END AS c37
  ```
- **Logic:** The under stock days flag is calculated by comparing stock days against a threshold (e.g., 15 days). A flag is returned depending on whether the stock days meet the criteria.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the under stock days flag, calculated based on predefined logic.

---

### c38: **Under Shipment Flag for the Current Month (当月残出荷予定数過少フラグ)**

- **Header Label:** `Under Shipment Flag for the Current Month (当月残出荷予定数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
  ```sql
  CASE
                        WHEN (V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY) < 0 THEN '◯'
                        WHEN V_SCREPORT.PASSED_STOCK_QTY < (V_SCREPORT.MONTH_PLNQTY - V_SCREPORT.MONTH_QTY) THEN '◯'
                        ELSE 'X'
                    END AS c38
  ```
- **Logic:** The under shipment flag for the current month is calculated by comparing planned and actual shipment quantities for the month. If the difference is below a threshold, a flag is returned.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the under shipment flag for the current month, calculated based on predefined logic.

---

### c39: **Short-Term Under-Planned Flag for the Following Month (翌月短期予定過少フラグ)**

- **Header Label:** `Short-Term Under-Planned Flag for the Following Month (翌月短期予定過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
  ```sql
  CASE
                        WHEN V_SCREPORT.PASSED_STOCK_QTY < (V_SCREPORT.MONTH_PLNQTY- MONTH_QTY + V_SCREPORT.NEXT_MONTH_PLNQTY) THEN '◯'
                        WHEN V_SCREPORT.MONTH_PLNQTY- MONTH_QTY < 0 THEN '◯'
                        WHEN  V_SCREPORT.PASSED_STOCK_QTY < V_SCREPORT.NEXT_MONTH_PLNQTY THEN '◯'
                        ELSE 'X'
                    END AS c39
  ```
- **Logic:** The short-term under-planned flag for the following month is calculated by comparing planned quantities for the current and next month against stock levels. A flag is returned based on the comparison.
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the short-term under-planned flag for the following month, calculated based on predefined logic.

---

### c40: **Judgment Report (成績書)**

- **Header Label:** `Judgment Report (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** The status of the judgment report is fetched from the T_HANTEI table by matching the JUDGE_ID. The CERTIFICATE_STATUS is returned as the result.
- **Source:**
  ```sql
  SELECT CERTIFICATE_STATUS FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.CERTIFICATE_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the status of the judgment report, fetched from the T_HANTEI table.

---

### c41: **Send Email (メール送信)**

- **Header Label:** `Send Email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** Whether an email has been sent is fetched from the T_HANTEI table by matching the JUDGE_ID. The SEND_MAIL_STATUS is returned as the result.
- **Source:**
  ```sql
  SELECT SEND_MAIL_STATUS FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.SEND_MAIL_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether an email has been sent, fetched from the T_HANTEI table.

---

### c42: **Date of NETP Judgment (NETP判定日)**

- **Header Label:** `Date of NETP Judgment (NETP判定日)`
- **Data Type:** `Date`
- **Custom render:** The date of the NETP judgment is fetched from the T_HANTEI table by matching the JUDGE_ID. The NETP_JUDGE_DATE is returned as the result.
- **Source:**
  ```sql
  SELECT NETP_JUDGE_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.NETP_JUDGE_DATE`
- **Validation:** `If null,「未」(not yet) is displayed.`
- **Options:** `N/A`
- **Remarks:** Displays the date of the NETP judgment, fetched from the T_HANTEI table.

---

### c43: **Last Update (最終更新日時)**

- **Header Label:** `Last Update (最終更新日時)`
- **Data Type:** `Datetime`
- **Custom render:** The last update time is fetched from the T_RESPONSE table by matching the RESPONSE_ID. The UPDATE_RECORD_TIME is returned as the result.
- **Source:**
  ```sql
  SELECT UPDATE_RECORD_TIME FROM T_RESPONSE WHERE RESPONSE_ID = :response_id;
  ```
- **Save Destination:** `N/A` (Not editable)
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the last update time, fetched from the T_RESPONSE table.

---------------------------------------------------------
---------------------------------------------------------


## Judgement List (Edit Mode)


### c16: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `The urgent sign is retrieved from the T_HANTEI table and M_DISPLAY_ITEM.ITEM_NO=2 by matching the JUDGE_ID. The URGENT_TYPE is returned as the urgent sign.`
- **Source:**
  ```sql
  SELECT URGENT_TYPE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_TYPE`
- **Validation:** ``
- **Options:** `0: 内製 , 1: 外製`
- **Remarks:** Displays the urgent sign, fetched from the T_HANTEI table.

---

### c17: **Urgent Request Date (急ぎ依頼日)**

- **Header Label:** `Urgent Request Date (急ぎ依頼日)`
- **Data Type:** `Date`
- **Custom render:** The urgent request date is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_REQ_DATE is returned as the urgent request date.
- **Source:**
  ```sql
  SELECT URGENT_REQ_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_REQ_DATE`
- **Validation:** `Set today's date when setting「急ぎサイン」(c16) . Required when input 「急ぎサイン」(c16)`
- **Options:** `N/A`
- **Remarks:** Displays the urgent request date, fetched from the T_HANTEI table.
---

### c18: **Desired Date of Urgent Judgment (急ぎ判定希望日)**

- **Header Label:** `Desired Date of Urgent Judgment (急ぎ判定希望日)`
- **Data Type:** `Date`
- **Custom render:** The desired date for urgent judgment is retrieved from the T_HANTEI table by matching the JUDGE_ID. The URGENT_JUDGE_REQ_DATE is returned as the desired judgment date.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_DATE`
- **Validation:** `When the「急ぎサイン」(c16) is other than 「1=急」(1=urgent),input is not possible. And input required when「急ぎサイン」(c16) is 「1=急」(1=urgent). `
- **Options:** `N/A`
- **Remarks:** Displays the desired date for the urgent judgment, fetched from the T_HANTEI table.

---

### c19: **Desired Time for Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time for Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** The desired time for urgent judgment is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_JUDGE_REQ_TIME is returned as the desired time for judgment.
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_TIME FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_JUDGE_REQ_TIME`
- **Validation:** `When the「急ぎサイン」(c16) is other than 「1=急」(1=urgent),input is not possible.`
- **Options:** `N/A`
- **Remarks:** Displays the desired time for the urgent judgment, fetched from the T_HANTEI table.

---

### c23: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** The attribute (color-coded) is fetched from the T_HANTEI table by matching the JUDGE_ID. The URGENT_ATTRIBUTE is returned as the attribute.
- **Source:**
  ```sql
  SELECT URGENT_ATTRIBUTE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.URGENT_ATTRIBUTE`
- **Validation:** `When 「急ぎサイン」(c16) is 「1=急」 (1=urgent), input required.`
- **Options:** `N/A`
- **Remarks:** Displays the attribute as color-coded information, fetched from the T_HANTEI table.

---

### c24: **Desired Movement Date (移動希望日)**

- **Header Label:** `Desired Movement Date (移動希望日)`
- **Data Type:** `Date`
- **Custom render:** `Date`
- **Source:**
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
- **Logic:** The desired movement date is calculated using logic based on the plant division name, urgent type, and other factors. It uses the calendar (ERP_CALEM) and the maximum date after considering the relevant conditions.
- **Save Destination:** `T_HANTEI.MOVE_REQ_DATE`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the desired movement date, calculated based on predefined logic.

---

### c25: **Evening Packing・Morning Delivery Sign (宵積サイン)**

- **Header Label:** `Evening Packing・Morning Delivery Sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `TinyInt`
- **Source:**
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
- **Logic:** The evening packing or morning delivery sign is calculated based on the plant division name and urgent type. It considers various factors, including response times and plant locations, and returns either a 0 or 1.
- **Save Destination:** `T_HANTEI.VESPER_FLAG`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the evening packing or morning delivery sign, calculated based on predefined logic.

---

### c31: **Destination/Delivery (移動先/納品先)**

- **Header Label:** `Destination/Delivery (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Source:**
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
- **Logic:** The destination or delivery name is determined either from the T_HANTEI or RSOS_M_LOCATION table based on whether the delivery destination is available or fetched from the inventory location.
- **Save Destination:** `T_HANTEI.DELIVERY_DESTINATION_NAME`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the destination or delivery name. If no data in T_HANTEI, it is fetched from RSOS_M_LOCATION.

---

### c33: **Whether Movement Ticket is Issued (移動票発行有無)**

- **Header Label:** `Whether Movement Ticket is Issued (移動票発行有無)`
- **Data Type:** `Date`
- **Custom render:** Whether the movement ticket is issued is fetched from the T_HANTEI table by matching the JUDGE_ID. The MOVE_TICKET_ISSUED is returned as the result.
- **Source:**
  ```sql
  SELECT MOVE_TICKET_ISSUED FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.MOVE_TICKET_ISSUED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement ticket has been issued, fetched from the T_HANTEI table.

---

### c34: **Completion of Movement (移動完了有無)**

- **Header Label:** `Completion of Movement (移動完了有無)`
- **Data Type:** `Date`
- **Custom render:** The completion of movement is fetched from the T_HANTEI table by matching the JUDGE_ID. The MOVE_FINISHED is returned as the result.
- **Source:**
  ```sql
  SELECT MOVE_FINISHED FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.MOVE_FINISHED`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether the movement has been completed, fetched from the T_HANTEI table.

---

### c40: **Judgment Report (成績書)**

- **Header Label:** `Judgment Report (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** The status of the judgment report is fetched from the T_HANTEI table by matching the JUDGE_ID. The CERTIFICATE_STATUS is returned as the result.
- **Source:**
  ```sql
  SELECT CERTIFICATE_STATUS FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.CERTIFICATE_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays the status of the judgment report, fetched from the T_HANTEI table.

---

### c41: **Send Email (メール送信)**

- **Header Label:** `Send Email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** Whether an email has been sent is fetched from the T_HANTEI table by matching the JUDGE_ID. The SEND_MAIL_STATUS is returned as the result.
- **Source:**
  ```sql
  SELECT SEND_MAIL_STATUS FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.SEND_MAIL_STATUS`
- **Validation:** `N/A`
- **Options:** `N/A`
- **Remarks:** Displays whether an email has been sent, fetched from the T_HANTEI table.

---

### c42: **Date of NETP Judgment (NETP判定日)**

- **Header Label:** `Date of NETP Judgment (NETP判定日)`
- **Data Type:** `Date`
- **Custom render:**  The date of the NETP judgment is fetched from the T_HANTEI table by matching the JUDGE_ID. The NETP_JUDGE_DATE is returned as the result.
- **Source:**
  ```sql
  SELECT NETP_JUDGE_DATE FROM T_HANTEI WHERE JUDGE_ID = :judge_id;
  ```
- **Save Destination:** `T_HANTEI.NETP_JUDGE_DATE`0
- **Validation:** `If null,「未」(not yet) is displayed.`
- **Options:** `N/A`
- **Remarks:** Displays the date of the NETP judgment, fetched from the T_HANTEI table.


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
  ```sql
  SELECT TANTO FROM cfg_kg00100_search_filters WHERE TANTO LIKE '%判定一覧検索条件.担当者%'
- **Remarks:** `This field allows the user to search for the person in charge.`

### s2-1: **In-house/Outsourcing (内製/外製)**

- **Header Label:** `In-house/Outsourcing (内製/外製)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c2`
- **search condition:** `= cfg_kg00100_search_filters.IN_OUT_SOURCING` (`= 判定一覧検索条件.内製/外製`)
- **Save Destination:** `cfg_kg00100_search_filters.IN_OUT_SOURCING`
- **Source:**
  ```sql
  SELECT IN_OUT_SOURCING FROM cfg_kg00100_search_filters WHERE IN_OUT_SOURCING = 判定一覧検索条件.内製/外製
- **Remarks:** `This field allows the user to search for whether the product is in-house or outsourced.`

### s3-1: **Item CD (基準品目CD)**

- **Header Label:** `Item CD (基準品目CD)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c3`
- **search condition:** `= cfg_kg00100_search_filters.ITEM_CODE` (`= 判定一覧検索条件.基準品目CD`)
- **Save Destination:** `cfg_kg00100_search_filters.ITEM_CODE`
- **Source:**
  ```sql
  SELECT ITEM_CODE FROM cfg_kg00100_search_filters WHERE ITEM_CODE = 判定一覧検索条件.基準品目CD
- **Remarks:** `This field allows the user to search based on the reference item code (基準品目CD).`

### s4-1: **Production Abbreviation (生産略称)**

- **Header Label:** `Production Abbreviation (生産略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c4`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.PRODUCT_SHORT_NAME%'` (`LIKE '%判定一覧検索条件.生産略称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.PRODUCT_SHORT_NAME`
- **Source:**
  ```sql
  SELECT PRODUCT_SHORT_NAME FROM cfg_kg00100_search_filters WHERE PRODUCT_SHORT_NAME LIKE '%判定一覧検索条件.生産略称%'
- **Remarks:** `This field allows the user to search based on the production abbreviation (生産略称).`

### s5-1: **Sales Abbreviation (販売略称)**

- **Header Label:** `Sales Abbreviation (販売略称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c5`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.SALES_SHORT_NAME%'` (`LIKE '%判定一覧検索条件.販売略称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.SALES_SHORT_NAME`
- **Source:**
  ```sql
  SELECT SALES_SHORT_NAME FROM cfg_kg00100_search_filters WHERE SALES_SHORT_NAME LIKE '%判定一覧検索条件.販売略称%'
- **Remarks:** `This field allows the user to search based on the sales abbreviation (販売略称).`

### s6-1: **Lot (ロット)**

- **Header Label:** `Lot (ロット)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c6`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.LOT%'` (`LIKE '%判定一覧検索条件.ロット%'`)
- **Save Destination:** `cfg_kg00100_search_filters.LOT`
- **Source:**
  ```sql
  SELECT LOT FROM cfg_kg00100_search_filters WHERE LOT LIKE '%判定一覧検索条件.ロット%'
- **Remarks:** `This field allows the user to search based on the lot number (ロット).`

### s7-1: **Delivery Date "from" (納品日from)**

- **Header Label:** `Delivery Date "from" (納品日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c7`
- **search condition:** `>= cfg_kg00100_search_filters.DELIVERY_DATE_FROM` (`>= 判定一覧検索条件.納品日from`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DATE_FROM`
- **Source:**
  ```sql
  SELECT DELIVERY_DATE FROM cfg_kg00100_search_filters WHERE DELIVERY_DATE >= 判定一覧検索条件.納品日from
- **Remarks:** `This field filters data by delivery date starting from a specific date.`

### s7-2: **Delivery Date "to" (納品日to)**

- **Header Label:** `Delivery Date "to" (納品日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c7`
- **search condition:** `<= cfg_kg00100_search_filters.DELIVERY_DATE_TO` (`<= 判定一覧検索条件.納品日to`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DATE_TO`
- **Source:**
  ```sql
  SELECT DELIVERY_DATE FROM cfg_kg00100_search_filters WHERE DELIVERY_DATE <= 判定一覧検索条件.納品日to
- **Remarks:** `This field filters data by delivery date up to a specific date.`

### s8-1: **Production Building/Outsourcing (生産棟/外製先)**

- **Header Label:** `Production Building/Outsourcing (生産棟/外製先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `for c8`
- **search condition:** `= cfg_kg00100_search_filters.PLANT_DIVISION_CODE` (`= 判定一覧検索条件.生産棟/外製先`)
- **Save Destination:** `cfg_kg00100_search_filters.PLANT_DIVISION_CODE`
- **Source:**
  ```sql
  SELECT PLANT_DIVISION_CODE FROM cfg_kg00100_search_filters WHERE PLANT_DIVISION_CODE = 判定一覧検索条件.生産棟/外製先
- **Remarks:** `This field filters data by the production building or outsourcing location.`

### s9-1: **Item Name (品目名称)**

- **Header Label:** `Item Name (品目名称)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c9`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.ITEM_NAME%'` (`LIKE '%判定一覧検索条件.品目名称%'`)
- **Save Destination:** `cfg_kg00100_search_filters.ITEM_NAME`
- **Source:**
  ```sql
  SELECT ITEM_NAME FROM cfg_kg00100_search_filters WHERE ITEM_NAME LIKE '%判定一覧検索条件.品目名称%'
- **Remarks:** `This field filters data by the item name using a partial match.`

### s10-1: **Date of Dispensing "from" (調合日from)**

- **Header Label:** `Date of Dispensing "from" (調合日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c10`
- **search condition:** `>= cfg_kg00100_search_filters.MIXTURE_DATE_FROM` (`>= 判定一覧検索条件.調合日from`)
- **Save Destination:** `cfg_kg00100_search_filters.MIXTURE_DATE_FROM`
- **Source:**
  ```sql
  SELECT MIXTURE_DATE_FROM FROM cfg_kg00100_search_filters WHERE MIXTURE_DATE_FROM >= 判定一覧検索条件.調合日from
- **Remarks:** `This field filters the results for the dispensing date starting from a specified date.`

### s10-2: **Date of Dispensing "to" (調合日to)**

- **Header Label:** `Date of Dispensing "to" (調合日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c10`
- **search condition:** `<= cfg_kg00100_search_filters.MIXTURE_DATE_TO` (`<= 判定一覧検索条件.調合日to`)
- **Save Destination:** `cfg_kg00100_search_filters.MIXTURE_DATE_TO`
- **Source:**
  ```sql
  SELECT MIXTURE_DATE_TO FROM cfg_kg00100_search_filters WHERE MIXTURE_DATE_TO <= 判定一覧検索条件.調合日to
- **Remarks:** `This field filters the results for the dispensing date up to a specified date.`

### s11-1: **Filling Date "from" (充填日from)**

- **Header Label:** `Filling Date "from" (充填日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c11`
- **search condition:** `>= cfg_kg00100_search_filters.FILL_DATE_FROM` (`>= 判定一覧検索条件.充填日from`)
- **Save Destination:** `cfg_kg00100_search_filters.FILL_DATE_FROM`
- **Source:**
  ```sql
  SELECT FILL_DATE_FROM FROM cfg_kg00100_search_filters WHERE FILL_DATE_FROM >= 判定一覧検索条件.充填日from
- **Remarks:** `This field filters the results starting from the specified filling date.`

### s11-2: **Filling Date "to" (充填日to)**

- **Header Label:** `Filling Date "to" (充填日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c11`
- **search condition:** `<= cfg_kg00100_search_filters.FILL_DATE_TO` (`<= 判定一覧検索条件.充填日to`)
- **Save Destination:** `cfg_kg00100_search_filters.FILL_DATE_TO`
- **Source:**
  ```sql
  SELECT FILL_DATE_TO FROM cfg_kg00100_search_filters WHERE FILL_DATE_TO <= 判定一覧検索条件.充填日to
- **Remarks:** `This field filters the results up to the specified filling date.`

### s12-1: **Packing Date "from" (包装日from)**

- **Header Label:** `Packing Date "from" (包装日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c12`
- **search condition:** `>= cfg_kg00100_search_filters.WRAP_DATE_FROM` (`>= 判定一覧検索条件.包装日from`)
- **Save Destination:** `cfg_kg00100_search_filters.WRAP_DATE_FROM`
- **Source:**
  ```sql
  SELECT WRAP_DATE_FROM FROM cfg_kg00100_search_filters WHERE WRAP_DATE_FROM >= 判定一覧検索条件.包装日from
- **Remarks:** `This field filters the results starting from the specified packing date.`

### s12-2: **Packing Date "to" (包装日to)**

- **Header Label:** `Packing Date "to" (包装日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c12`
- **search condition:** `<= cfg_kg00100_search_filters.WRAP_DATE_TO` (`<= 判定一覧検索条件.包装日to`)
- **Save Destination:** `cfg_kg00100_search_filters.WRAP_DATE_TO`
- **Source:**
  ```sql
  SELECT WRAP_DATE_TO FROM cfg_kg00100_search_filters WHERE WRAP_DATE_TO <= 判定一覧検索条件.包装日to
- **Remarks:** `This field filters the results up to the specified packing date.`

### s13-1: **Usual Judgment Date "from" (通常判定日from)**

- **Header Label:** `Usual Judgment Date "from" (通常判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c14`
- **search condition:** `>= cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_FROM` (`>= 判定一覧検索条件.通常判定日from`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_FROM`
- **Source:**
  ```sql
  SELECT NORMAL_JUDGE_DATE_FROM FROM cfg_kg00100_search_filters WHERE NORMAL_JUDGE_DATE_FROM >= 判定一覧検索条件.通常判定日from
- **Remarks:** `This field filters the results from the specified usual judgment date onward.`

### s13-2: **Usual Judgment Date "to" (通常判定日to)**

- **Header Label:** `Usual Judgment Date "to" (通常判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c14`
- **search condition:** `<= cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_TO` (`<= 判定一覧検索条件.通常判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_JUDGE_DATE_TO`
- **Source:**
  ```sql
  SELECT NORMAL_JUDGE_DATE_TO FROM cfg_kg00100_search_filters WHERE NORMAL_JUDGE_DATE_TO <= 判定一覧検索条件.通常判定日to
- **Remarks:** `This field filters the results up to the specified usual judgment date.`

### s14-1: **Test Status (試験ステータス)**

- **Header Label:** `Test Status (試験ステータス)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c15`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.INSPECTION_STATUS%'` (`LIKE '%判定一覧検索条件.試験ステータス%'`)
- **Save Destination:** `cfg_kg00100_search_filters.INSPECTION_STATUS`
- **Source:**
  ```sql
  SELECT INSPECTION_STATUS FROM cfg_kg00100_search_filters WHERE INSPECTION_STATUS LIKE '%判定一覧検索条件.試験ステータス%'
- **Remarks:** `Filters the data based on the inspection status, allowing for partial matches.`

### s15-1: **Urgent Sign (急ぎサイン)**

- **Header Label:** `Urgent Sign (急ぎサイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c16`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_TYPE` (`= 判定一覧検索条件.急ぎサイン`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_TYPE`
- **Source:**
  ```sql
  SELECT URGENT_TYPE FROM cfg_kg00100_search_filters WHERE URGENT_TYPE = 判定一覧検索条件.急ぎサイン
- **Remarks:** `Filters the data based on the urgent sign type, using an exact match.`

### s16-1: **Urgent Request Date "from" (急ぎ依頼日from)**

- **Header Label:** `Urgent Request Date "from" (急ぎ依頼日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c17`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_REQ_DATE_FROM` (`>= 判定一覧検索条件.急ぎ依頼日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_REQ_DATE_FROM`
- **Source:**
  ```sql
  SELECT URGENT_REQ_DATE FROM cfg_kg00100_search_filters WHERE URGENT_REQ_DATE >= 判定一覧検索条件.急ぎ依頼日from
- **Remarks:** `Filters the data by selecting records where the urgent request date is greater than or equal to the specified start date.`

### s16-2: **Urgent Request Date "to" (急ぎ依頼日to)**

- **Header Label:** `Urgent Request Date "to" (急ぎ依頼日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c17`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_REQ_DATE_TO` (`<= 判定一覧検索条件.急ぎ依頼日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_REQ_DATE_TO`
- **Source:**
  ```sql
  SELECT URGENT_REQ_DATE FROM cfg_kg00100_search_filters WHERE URGENT_REQ_DATE <= 判定一覧検索条件.急ぎ依頼日to
- **Remarks:** `Filters the data by selecting records where the urgent request date is less than or equal to the specified end date.`

### s17-1: **Desired Date of Urgent Judgment "from" (急ぎ判定希望日from)**

- **Header Label:** `Desired Date of Urgent Judgment "from" (急ぎ判定希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c18`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_FROM` (`>= 判定一覧検索条件.急ぎ判定希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_FROM`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_DATE FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_REQ_DATE >= 判定一覧検索条件.急ぎ判定希望日from
- **Remarks:** `Filters the data by selecting records where the desired date of urgent judgment is greater than or equal to the specified start date.`

### s17-2: **Desired Date of Urgent Judgment "to" (急ぎ判定希望日to)**

- **Header Label:** `Desired Date of Urgent Judgment "to" (急ぎ判定希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c18`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_TO` (`<= 判定一覧検索条件.急ぎ判定希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_DATE_TO`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_DATE FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_REQ_DATE <= 判定一覧検索条件.急ぎ判定希望日to
- **Remarks:** `Filters the data by selecting records where the desired date of urgent judgment is less than or equal to the specified end date.`

### s18-1: **Desired Time of Urgent Judgment (急ぎ判定希望時間)**

- **Header Label:** `Desired Time of Urgent Judgment (急ぎ判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c19`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_REQ_TIME` (`= 判定一覧検索条件.急ぎ判定希望時間`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_REQ_TIME`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_REQ_TIME FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_REQ_TIME = 判定一覧検索条件.急ぎ判定希望時間
- **Remarks:** `Filters the data based on the exact desired time for urgent judgment.`

### s19-1: **Quality Department Reply (品質部門の返信)**

- **Header Label:** `Quality Department Reply (品質部門の返信)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c20`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_RESP` (`= 判定一覧検索条件.品質部門の返信`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_RESP = 判定一覧検索条件.品質部門の返信
- **Remarks:** `Filters data based on the response from the quality department.`

### s20-1: **Corrected Judgment Date From (修正判定日from)**

- **Header Label:** `Corrected Judgment Date From (修正判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c21`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_FROM` (`>= 判定一覧検索条件.修正判定日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_FROM`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP_ANS_DATE FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_RESP_ANS_DATE >= 判定一覧検索条件.修正判定日from
- **Remarks:** `Filters data to show results from the corrected judgment date onward.`

### s20-2: **Corrected Judgment Date To (修正判定日to)**

- **Header Label:** `Corrected Judgment Date To (修正判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c21`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_TO` (`<= 判定一覧検索条件.修正判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_DATE_TO`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP_ANS_DATE FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_RESP_ANS_DATE <= 判定一覧検索条件.修正判定日to
- **Remarks:** `Filters data to show results up to the corrected judgment date.`

### s21-1: **Correct Judgment Time (修正判定時間)**

- **Header Label:** `Correct Judgment Time (修正判定時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `for c21`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_TIME` (`= 判定一覧検索条件.修正判定時間`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_JUDGE_RESP_ANS_TIME`
- **Source:**
  ```sql
  SELECT URGENT_JUDGE_RESP_ANS_TIME FROM cfg_kg00100_search_filters WHERE URGENT_JUDGE_RESP_ANS_TIME = 判定一覧検索条件.修正判定時間
- **Remarks:** `Filters data based on the exact corrected judgment time.`

### s22-1: **Attributes (Color-Coded) (属性（色分け）)**

- **Header Label:** `Attributes (Color-Coded) (属性（色分け）)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c23`
- **search condition:** `= cfg_kg00100_search_filters.URGENT_ATTRIBUTE` (`= 判定一覧検索条件.属性（色分け）`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_ATTRIBUTE`
- **Source:**
  ```sql
  SELECT URGENT_ATTRIBUTE FROM cfg_kg00100_search_filters WHERE URGENT_ATTRIBUTE = 判定一覧検索条件.属性（色分け）
- **Remarks:** `Filters data based on the color-coded attributes.`

### s23-1: **Moving Hope Day from (移動希望日from)**

- **Header Label:** `Moving Hope Day from (移動希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c24`
- **search condition:** `>= cfg_kg00100_search_filters.MOVE_REQ_DATE_FROM` (`>= 判定一覧検索条件.移動希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_REQ_DATE_FROM`
- **Source:**
  ```sql
  SELECT MOVE_REQ_DATE FROM cfg_kg00100_search_filters WHERE MOVE_REQ_DATE >= 判定一覧検索条件.移動希望日from
- **Remarks:** `Filters data by selecting records with a move request date starting from the specified date.`

### s23-2: **Moving Hope Day to (移動希望日to)**

- **Header Label:** `Moving Hope Day to (移動希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c24`
- **search condition:** `<= cfg_kg00100_search_filters.MOVE_REQ_DATE_TO` (`<= 判定一覧検索条件.移動希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_REQ_DATE_TO`
- **Source:**
  ```sql
  SELECT MOVE_REQ_DATE FROM cfg_kg00100_search_filters WHERE MOVE_REQ_DATE <= 判定一覧検索条件.移動希望日to
- **Remarks:** `Filters data by selecting records with a move request date up to the specified date.`

### s24-1: **Yoizumi sign (宵積サイン)**

- **Header Label:** `Yoizumi sign (宵積サイン)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c25`
- **search condition:** `= cfg_kg00100_search_filters.VESPER_FLAG` (`= 判定一覧検索条件.宵積サイン`)
- **Save Destination:** `cfg_kg00100_search_filters.VESPER_FLAG`
- **Source:**
  ```sql
  SELECT VESPER_FLAG FROM cfg_kg00100_search_filters WHERE VESPER_FLAG = 判定一覧検索条件.宵積サイン
- **Remarks:** `Filters data based on whether the Yoizumi (evening packing) sign is flagged or not.`

### s25-1: **Usually the possible date of delivery is from (通常出荷可能日from)**

- **Header Label:** `Usually the possible date of delivery is from (通常出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c26`
- **search condition:** `>= cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.通常出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_FROM`
- **Source:**
  ```sql
  SELECT NORMAL_SHIP_POSSIBLE_DATE_FROM 
  FROM cfg_kg00100_search_filters 
  WHERE NORMAL_SHIP_POSSIBLE_DATE_FROM >= 判定一覧検索条件.通常出荷可能日from
- **Remarks:** `Filters records where the usual available date for shipment is greater than or equal to the specified date.`

### s25-2: **Normal shipping date to (通常出荷可能日to)**

- **Header Label:** `Normal shipping date to (通常出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c26`
- **search condition:** `<= cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.通常出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NORMAL_SHIP_POSSIBLE_DATE_TO`
- **Source:**
  ```sql
  SELECT NORMAL_SHIP_POSSIBLE_DATE_TO 
  FROM cfg_kg00100_search_filters 
  WHERE NORMAL_SHIP_POSSIBLE_DATE_TO <= 判定一覧検索条件.通常出荷可能日to
- **Remarks:** `Filters records where the usual available date for shipment is less than or equal to the specified date.`

### s26-1: **Expedited shipping date from (急ぎ出荷可能日from)**

- **Header Label:** `Expedited shipping date from (急ぎ出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c27`
- **search condition:** `>= cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.急ぎ出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_FROM`
- **Source:**
  ```sql
  SELECT URGENT_SHIP_POSSIBLE_DATE_FROM 
  FROM cfg_kg00100_search_filters 
  WHERE URGENT_SHIP_POSSIBLE_DATE_FROM >= 判定一覧検索条件.急ぎ出荷可能日from
- **Remarks:** `Filters records where the expedited shipping date is greater than or equal to the specified date.`

### s26-2: **Expedited shipping date to (急ぎ出荷可能日to)**

- **Header Label:** `Expedited shipping date to (急ぎ出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c27`
- **search condition:** `<= cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.急ぎ出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.URGENT_SHIP_POSSIBLE_DATE_TO`
- **Source:**
  ```sql
  SELECT URGENT_SHIP_POSSIBLE_DATE_TO 
  FROM cfg_kg00100_search_filters 
  WHERE URGENT_SHIP_POSSIBLE_DATE_TO <= 判定一覧検索条件.急ぎ出荷可能日to
- **Remarks:** `Filters records where the expedited shipping date is less than or equal to the specified date.`

### s27-1: **Relaxed shipping date from (緩め出荷可能日from)**

- **Header Label:** `Relaxed shipping date from (緩め出荷可能日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c28`
- **search condition:** `>= cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_FROM` (`>= 判定一覧検索条件.緩め出荷可能日from`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_FROM`
- **Source:**
  ```sql
  SELECT LATE_SHIP_POSSIBLE_DATE_FROM 
  FROM cfg_kg00100_search_filters 
  WHERE LATE_SHIP_POSSIBLE_DATE_FROM >= 判定一覧検索条件.緩め出荷可能日from
- **Remarks:** `Filters records where the relaxed shipping date is greater than or equal to the specified date.`

### s27-2: **Relaxed shipping date to (緩め出荷可能日to)**

- **Header Label:** `Relaxed shipping date to (緩め出荷可能日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c28`
- **search condition:** `<= cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_TO` (`<= 判定一覧検索条件.緩め出荷可能日to`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_POSSIBLE_DATE_TO`
- **Source:**
  ```sql
  SELECT LATE_SHIP_POSSIBLE_DATE_TO 
  FROM cfg_kg00100_search_filters 
  WHERE LATE_SHIP_POSSIBLE_DATE_TO <= 判定一覧検索条件.緩め出荷可能日to
- **Remarks:** `Filters records where the relaxed shipping date is less than or equal to the specified date.`

### s28-1: **Desired date for loosening judgment from (緩め判定希望日from)**

- **Header Label:** `Desired date for loosening judgment from (緩め判定希望日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c29`
- **search condition:** `>= cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_FROM` (`>= 判定一覧検索条件.緩め判定希望日from`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_FROM`
- **Source:**
  ```sql
  SELECT LATE_SHIP_JUDGE_REQ_DATE_FROM 
  FROM cfg_kg00100_search_filters 
  WHERE LATE_SHIP_JUDGE_REQ_DATE_FROM >= 判定一覧検索条件.緩め判定希望日from
- **Remarks:** `Filters records where the desired date for loosening judgment is greater than or equal to the specified date.`

### s28-2: **Desired date for loosening judgment to (緩め判定希望日to)**

- **Header Label:** `Desired date for loosening judgment to (緩め判定希望日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c29`
- **search condition:** `<= cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_TO` (`<= 判定一覧検索条件.緩め判定希望日to`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_DATE_TO`
- **Source:**
  ```sql
  SELECT LATE_SHIP_JUDGE_REQ_DATE_TO 
  FROM cfg_kg00100_search_filters 
  WHERE LATE_SHIP_JUDGE_REQ_DATE_TO <= 判定一覧検索条件.緩め判定希望日to
- **Remarks:** `Filters records where the desired date for loosening judgment is less than or equal to the specified date.`

### s29-1: **Desired loosening judgment time (緩め判定希望時間)**

- **Header Label:** `Desired loosening judgment time (緩め判定希望時間)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c30`
- **search condition:** `= cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_TIME` (`= 判定一覧検索条件.緩め判定希望時間`)
- **Save Destination:** `cfg_kg00100_search_filters.LATE_SHIP_JUDGE_REQ_TIME`
- **Source:**
  ```sql
  SELECT LATE_SHIP_JUDGE_REQ_TIME 
  FROM cfg_kg00100_search_filters 
  WHERE LATE_SHIP_JUDGE_REQ_TIME = 判定一覧検索条件.緩め判定希望時間
- **Remarks:** `Filters records by the exact desired loosening judgment time.`

### s30-1: **Moving destination/delivery destination (移動先/納品先)**

- **Header Label:** `Moving destination/delivery destination (移動先/納品先)`
- **Data Type:** `Varchar`
- **Custom render:** `String`
- **Filter column:** `c31`
- **search condition:** `LIKE '%cfg_kg00100_search_filters.DELIVERY_DESTINATION%'` (`LIKE '%判定一覧検索条件.移動先/納品先%'`)
- **Save Destination:** `cfg_kg00100_search_filters.DELIVERY_DESTINATION`
- **Source:**
  ```sql
  SELECT DELIVERY_DESTINATION 
  FROM cfg_kg00100_search_filters 
  WHERE DELIVERY_DESTINATION LIKE '%判定一覧検索条件.移動先/納品先%'
- **Remarks:** `Filters records by matching the moving or delivery destination.`

### s31-1: **Issuance of transfer ticket? (移動票発行有無)**

- **Header Label:** `Issuance of transfer ticket? (移動票発行有無)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c33`
- **search condition:** `= cfg_kg00100_search_filters.MOVE_TICKET_ISSUED` (`= 判定一覧検索条件.移動票発行有無`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_TICKET_ISSUED`
- **Source:**
  ```sql
  SELECT MOVE_TICKET_ISSUED 
  FROM cfg_kg00100_search_filters 
  WHERE MOVE_TICKET_ISSUED = 判定一覧検索条件.移動票発行有無
- **Remarks:** `Filters records based on whether the transfer ticket has been issued.`

### s32-1: **Is the move complete? (移動完了有無)**

- **Header Label:** `Is the move complete? (移動完了有無)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c34`
- **search condition:** `= cfg_kg00100_search_filters.MOVE_FINISHED` (`= 判定一覧検索条件.移動完了有無`)
- **Save Destination:** `cfg_kg00100_search_filters.MOVE_FINISHED`
- **Source:**
  ```sql
  SELECT MOVE_FINISHED 
  FROM cfg_kg00100_search_filters 
  WHERE MOVE_FINISHED = 判定一覧検索条件.移動完了有無
- **Remarks:** `Filters records based on whether the movement has been completed.`

### s33-1: **Multi-location inventory flag (複数拠点在庫フラグ)**

- **Header Label:** `Multi-location inventory flag (複数拠点在庫フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c35`
- **search condition:** `= cfg_kg00100_search_filters.MULTIPLE_PLANT_INV_STATUS` (`= 判定一覧検索条件.複数拠点在庫フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.MULTIPLE_PLANT_INV_STATUS`
- **Source:**
  ```sql
  SELECT MULTIPLE_PLANT_INV_STATUS 
  FROM cfg_kg00100_search_filters 
  WHERE MULTIPLE_PLANT_INV_STATUS = 判定一覧検索条件.複数拠点在庫フラグ
- **Remarks:** `Filters records based on the multi-location inventory flag status.`

### s34-1: **Insufficient inventory days flag (在庫日数過少フラグ)**

- **Header Label:** `Insufficient inventory days flag (在庫日数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c37`
- **search condition:** `= cfg_kg00100_search_filters.INV_DAYS_SHORT` (`= 判定一覧検索条件.在庫日数過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.INV_DAYS_SHORT`
- **Source:**
  ```sql
  SELECT INV_DAYS_SHORT 
  FROM cfg_kg00100_search_filters 
  WHERE INV_DAYS_SHORT = 判定一覧検索条件.在庫日数過少フラグ
- **Remarks:** `Filters records based on the insufficient inventory days flag.`

### s35-1: **Insufficient number of scheduled shipments remaining for this month flag (当月残出荷予定数過少フラグ)**

- **Header Label:** `Insufficient number of scheduled shipments remaining for this month flag (当月残出荷予定数過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c38`
- **search condition:** `= cfg_kg00100_search_filters.CURRENT_MONTH_PLAN_SHORT` (`= 判定一覧検索条件.当月残出荷予定数過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.CURRENT_MONTH_PLAN_SHORT`
- **Source:**
  ```sql
  SELECT CURRENT_MONTH_PLAN_SHORT 
  FROM cfg_kg00100_search_filters 
  WHERE CURRENT_MONTH_PLAN_SHORT = 判定一覧検索条件.当月残出荷予定数過少フラグ
- **Remarks:** `Filters records based on the insufficient number of scheduled shipments remaining for this month.`

### s36-1: **Short-term underscheduled flag for next month (翌月短期予定過少フラグ)**

- **Header Label:** `Short-term underscheduled flag for next month (翌月短期予定過少フラグ)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c39`
- **search condition:** `= cfg_kg00100_search_filters.NEXT_MONTH_PLAN_SHORT` (`= 判定一覧検索条件.翌月短期予定過少フラグ`)
- **Save Destination:** `cfg_kg00100_search_filters.NEXT_MONTH_PLAN_SHORT`
- **Source:**
  ```sql
  SELECT NEXT_MONTH_PLAN_SHORT 
  FROM cfg_kg00100_search_filters 
  WHERE NEXT_MONTH_PLAN_SHORT = 判定一覧検索条件.翌月短期予定過少フラグ
- **Remarks:** `Filters records based on the short-term underscheduled flag for the following month.`

### s37-1: **Report card (成績書)**

- **Header Label:** `Report card (成績書)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c40`
- **search condition:** `= cfg_kg00100_search_filters.CERTIFICATE_STATUS` (`= 判定一覧検索条件.成績書`)
- **Save Destination:** `cfg_kg00100_search_filters.CERTIFICATE_STATUS`
- **Source:**
  ```sql
  SELECT CERTIFICATE_STATUS 
  FROM cfg_kg00100_search_filters 
  WHERE CERTIFICATE_STATUS = 判定一覧検索条件.成績書
- **Remarks:** `Filters records based on the report card status.`

### s38-1: **Send email (メール送信)**

- **Header Label:** `Send email (メール送信)`
- **Data Type:** `TinyInt`
- **Custom render:** `String`
- **Filter column:** `c41`
- **search condition:** `= cfg_kg00100_search_filters.SEND_MAIL_STATUS` (`= 判定一覧検索条件.メール送信`)
- **Save Destination:** `cfg_kg00100_search_filters.SEND_MAIL_STATUS`
- **Source:**
  ```sql
  SELECT SEND_MAIL_STATUS 
  FROM cfg_kg00100_search_filters 
  WHERE SEND_MAIL_STATUS = 判定一覧検索条件.メール送信
- **Remarks:** `Filters records based on the email send status.`

### s39-1: **NETP decision date from (NETP判定日from)**

- **Header Label:** `NETP decision date from (NETP判定日from)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c42`
- **search condition:** `>= cfg_kg00100_search_filters.NETP_JUDGE_DATE_FROM` (`>= 判定一覧検索条件.NETP判定日from`)
- **Save Destination:** `cfg_kg00100_search_filters.NETP_JUDGE_DATE_FROM`
- **Source:**
  ```sql
  SELECT NETP_JUDGE_DATE 
  FROM cfg_kg00100_search_filters 
  WHERE NETP_JUDGE_DATE >= 判定一覧検索条件.NETP判定日from
- **Remarks:** `Filters records based on the NETP decision date starting from the specified value.`

### s39-2: **NETP judgment date to (NETP判定日to)**

- **Header Label:** `NETP judgment date to (NETP判定日to)`
- **Data Type:** `Date`
- **Custom render:** `String`
- **Filter column:** `c43`
- **search condition:** `<= cfg_kg00100_search_filters.NETP_JUDGE_DATE_TO` (`<= 判定一覧検索条件.NETP判定日to`)
- **Save Destination:** `cfg_kg00100_search_filters.NETP_JUDGE_DATE_TO`
- **Source:**
  ```sql
  SELECT NETP_JUDGE_DATE 
  FROM cfg_kg00100_search_filters 
  WHERE NETP_JUDGE_DATE <= 判定一覧検索条件.NETP判定日to
- **Remarks:** `Filters records based on the NETP judgment date ending with the specified value.`
































