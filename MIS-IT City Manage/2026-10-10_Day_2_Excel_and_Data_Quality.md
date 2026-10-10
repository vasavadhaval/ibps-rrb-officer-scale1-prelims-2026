# 10 ઓક્ટોબર 2026 — દિવસ 2: Excel અને સાચું MIS Reporting

આજનું લક્ષ્ય: Ward ના રેકોર્ડ પરથી ચકાસેલો Report બનાવવો અને તમે કરેલી તપાસ સમજાવવી.

## અભ્યાસનો ક્રમ — આશરે ચાર કલાક

- [ ] 30 મિનિટ: પોતાનો પરિચય અને ગઈકાલના MIS જવાબો મોટેથી બોલો.
- [ ] 90 મિનિટ: Formulas, Lookup, Cleaning, PivotTable અને Chart ની પ્રેક્ટિસ કરો.
- [ ] 45 મિનિટ: સાચું Reporting અને Portal workflow શીખો.
- [ ] 45 મિનિટ: Answer key વાંચતાં પહેલાં Assignment કરો.
- [ ] 30 મિનિટ: આજના Interview પ્રશ્નોના જવાબ બોલો.

બે કલાક જ હોય તો 90 મિનિટ Excel/Assignment અને 30 મિનિટ Data quality ના જવાબો માટે આપો. ગઈકાલની Sheet વાપરો અથવા નીચેનો Data નાખો.

## Excel — જાતે કરીને શીખો

આ Dataset અને Exercises **કાલ્પનિક છે; રાજપીપળાનો સાચો Data નથી**.

### A. Dataset દાખલ કરો

`Practice` નામની Sheet માં A1:H7 સુધી નીચેનો Data નાખો. એક જ Column માં આવે તો **Data → Text to Columns → Delimited → Comma** વાપરો. અલગ File Download કરવાની જરૂર નથી.

```text
Date,Ward,Households,Covered,Segregating,WasteKg,ProcessedKg,Complaints
2026-10-09,1,200,180,140,500,400,5
2026-10-09,2,300,270,200,700,560,8
2026-10-09,3,250,225,175,600,450,4
2026-10-10,1,200,190,150,520,430,3
2026-10-10,2,300,260,195,680,540,7
2026-10-10,3,250,230,180,610,480,5
```

આ Exercise માં:

- `Covered`: તે દિવસે સેવા મળેલા ઘરો.
- `Segregating`: Covered ઘરોમાંથી કચરો અલગ કરતા ઘરો.
- `WasteKg`: તે દિવસે એકત્ર કરેલો કચરો, kg માં.
- `ProcessedKg`: તે દિવસના Collection માંથી Process થયેલો ભાગ.

વાસ્તવિક Reporting માં કચેરીની વ્યાખ્યા અનુસરો. Processing માં જૂનો Stock પણ હોઈ શકે અને Collection એ Generation નથી. એક જ Ward ના ઘરો બે તારીખે દર્શાવ્યા છે; બંને દિવસનું Households ઉમેરવાથી **household-day observations** મળે, Unique households નહીં.

### B. Basic formulas

I1 માં `Coverage` અને J1 માં `SegregationAmongCovered` લખો.

```excel
=IF(C2=0,"Check denominator",D2/C2)
=IF(D2=0,"Check denominator",E2/D2)
```

પહેલો Formula I2 અને બીજો J2 માં નાખો; Row 7 સુધી Fill down કરો. યોગ્ય આંકડાને Percentage format આપો. **Percentage format આપો ત્યારે ફરી ×100 ન કરો.** “Check denominator” એટલે ભાગાકારમાં નીચેની સંખ્યા 0 છે અને તપાસ જરૂરી છે.

પ્રેક્ટિસ માટે Formulas:

```excel
=SUM(F2:F7)
=AVERAGE(F2:F7)
=MAX(H2:H7)
=MIN(H2:H7)
=COUNT(F2:F7)
=COUNTA(B2:B7)
=COUNTIF(B2:B7,2)
=SUMIF(B2:B7,2,F2:F7)
=SUMIFS(F2:F7,B2:B7,2)
=COUNTIFS(B2:B7,2,H2:H7,">5")
```

ક્રમ પ્રમાણે તેમનાં જવાબ અને ઉપયોગ:

1. **SUM:** કુલ Waste **3610 kg**.
2. **AVERAGE:** દરેક Row નો સરેરાશ Waste આશરે **601.67 kg**.
3. **MAX:** સૌથી વધુ Complaints **8**.
4. **MIN:** સૌથી ઓછી Complaints **3**.
5. **COUNT:** Number ધરાવતા Cells **6**.
6. **COUNTA:** ખાલી ન હોય તેવા Ward cells **6**.
7. **COUNTIF:** Ward 2 ની Rows **2**.
8. **SUMIF:** Ward 2 નો Waste **1380 kg**.
9. **SUMIFS:** અહીં એક જ શરતથી ફરી **1380 kg**.
10. **COUNTIFS:** Ward 2 માં Complaints 5 કરતાં વધુ હોય તેવી Rows **2**.

**COUNT** Numbers ગણે; **COUNTA** ખાલી ન હોય તેવા Cells ગણે. **SUMIF** એક શરત પ્રમાણે અને **SUMIFS** એક અથવા વધુ શરત પ્રમાણે સરવાળો કરે. SUMIFS માં Sum range પહેલાં આવે અને બધા Ranges ની Rows/Columns મેળ ખાતાં હોવા જોઈએ. [Microsoft SUMIFS reference](https://support.microsoft.com/en-us/excel/functions/sumifs-function).

બે શરત માટે L2 માં 9 ઓક્ટોબર 2026 ની સાચી **Excel date** નાખો:

```excel
=SUMIFS(F2:F7,B2:B7,2,A2:A7,L2)
```

જવાબ **700 kg** આવવો જોઈએ, જો A Column અને L2 ની Date values મેળ ખાતી હોય. Date જો Text તરીકે હોય તો Formula 0 આપી શકે. અણધાર્યું પરિણામ આવે ત્યારે Data type તપાસો.

### C. Lookup — Ward નું નામ શોધવું

N2:N4 માં Ward IDs **1, 2, 3** અને O2:O4 માં કાલ્પનિક નામો **Ward One, Ward Two, Ward Three** લખો.

```excel
=XLOOKUP(B2,$N$2:$N$4,$O$2:$O$4,"Not found")
=IFERROR(VLOOKUP(B2,$N$2:$O$4,2,FALSE),"Not found")
```

આ બે વિકલ્પ છે; બંને સાથે વાપરવાની જરૂર નથી.

- **XLOOKUP** Excel 2016/2019 માં નથી; ત્યાં **VLOOKUP** વાપરી શકો.
- VLOOKUP માં **FALSE** એટલે Exact match.
- VLOOKUP માટે Lookup ID તેના Range ના પહેલા Column માં હોવો જોઈએ.
- **$** Reference ને સ્થિર રાખે છે, જેથી Formula Copy કરતી વખતે બદલાય નહીં.

[Microsoft XLOOKUP reference](https://support.microsoft.com/en-gb/excel/functions/xlookup-function).

**IFERROR** થી સાચી Reporting error છુપાવશો નહીં. Zero વાસ્તવિક મૂલ્ય હોઈ શકે; “Not found” એટલે Match નથી મળ્યો, તેથી તપાસ જરૂરી છે.

### D. Sort, Filter, Cleaning અને Validation

1. ફેરફાર પહેલાં Raw copy સાચવો.
2. આખો Dataset પસંદ કરીને Sort કરો, જેથી Columns અલગ ન પડી જાય.
3. Ward 2 Filter કરો; **બે Rows** હોવી જોઈએ.
4. Date અને Number ના Types તપાસો. Phone/ID માં આગળ 0 જરૂરી હોય તો તેને Text તરીકે રાખો.
5. ખૂટતા Mandatory fields અને અણધાર્યા આંકડા Flag કરો.
6. આ Exercise માં `Covered <= Households`, `Segregating <= Covered` અને આંકડા Negative નથી તે તપાસો.
7. Duplicate માટે Unique key નક્કી કરો. અહીં **Date + Ward**; સાચા System માં Route/Shift પણ હોઈ શકે.
8. અલગ તારીખના એક જ Ward ની Rows Delete ન કરો; તે સાચા અલગ Records છે.

`=TRIM(K2)` સામાન્ય વધારાની Spaces દૂર કરે છે, બધા Hidden Unicode characters નહીં. Standard Ward IDs અને અધિકૃત Master list વાપરો. Drop-down validation થી જુદી Spelling ઓછી થઈ શકે. **Conditional formatting** Missing અથવા Low coverage બતાવે છે; Source documents ની તપાસનું સ્થાન લેતું નથી.

### E. PivotTable અને Chart બનાવો

**A1:H7 પસંદ કરો → Insert → PivotTable.**

- **Rows:** Ward.
- **Values:** WasteKg અને ProcessedKg.
- **Filters:** Date.
- Numbers માટે **Sum** છે કે **Count** તે તપાસો.
- 9 ઓક્ટોબર Filter કરો: કુલ Waste **1800 kg**.
- Source data બદલાય પછી **Refresh** કરો.

PivotTable મૂળ Records બદલી નાખ્યા વગર Ward/Date પ્રમાણે Summary આપે છે. [Microsoft PivotTable reference](https://support.microsoft.com/en-us/excel/sum-values-in-a-pivottable).

એક તારીખ માટે Ward-wise Collected અને Processed kg નો Column chart બનાવો. Title, Date અને Units આપો. સમજાવ્યા વગર એક Axis પર kg અને % ભેગાં ન કરો.

### F. Percentage ગણતાં શું ધ્યાન રાખવું?

- **Collection coverage:** એક જ સમયગાળા/વિસ્તારમાં Covered households / Eligible households.
- **Segregation:** નિયત Denominator લો; આ Exercise માં Segregating / Covered.
- **Complaint closure:** નક્કી કરેલા ફરિયાદોના સમૂહમાં Resolved / Received. જૂનો Backlog હોય તો તેનો આધાર સ્પષ્ટ કરો.
- **Waste processing:** અધિકૃત Indicator ની વ્યાખ્યા લો. Processing / Generation અને Processing / Collection જુદાં છે.

Ward ના કદ જુદા હોય ત્યારે Ward percentages ની સીધી Average ન લો. **કુલ Numerator / કુલ Denominator** લો. Numerator એટલે ભાગાકારમાં ઉપરની સંખ્યા; Denominator એટલે નીચેની આધાર સંખ્યા.

## સાચું MIS Reporting અને Portal પર કામ

### યાદ રાખવાનો Workflow

**Collect → Validate → Reconcile → Approval → Submit → Evidence → Follow-up.**

ગુજરાતીમાં: **એકત્ર કરો → ચકાસો → તફાવત મેળવો → મંજૂરી લો → મોકલો → પુરાવા સાચવો → આગળની કાર્યવાહી તપાસો.**

ઉદાહરણ: Field staff પાસેથી Ward report, Collection register અને Weighing record મળે. તારીખ, Ward, Units અને સંપૂર્ણતા તપાસો. Totals સરખાવો અને તફાવતનું કારણ પૂછીને સુધારો નોંધો. Report Review માટે આપો; મંજૂરી પછી અધિકૃત Account થી Upload કરો અને Acknowledgement સાચવો.

Submit કરતાં પહેલાં પૂછો:

- સમયગાળો, Ward IDs અને Units સાચાં છે?
- Missing record ને Pending બતાવ્યો છે, Zero નહીં?
- Totals માટે Register/Weighing slip જેવા Source proof છે?
- Repeated record સાચો છે કે Duplicate?
- મોટો ફેરફાર હોય તો તેનું કારણ સમજાવ્યું છે?
- Upload અને Reviewed report ના આંકડા સરખાં છે?
- Photo/Documents વાંચી શકાય તેવાં અને યોગ્ય Activity સાથે જોડાયેલાં છે?
- જરૂરી હોય ત્યાં અધિકારીએ મંજૂરી આપી છે?
- Submission reference અને Final version Save કર્યા છે?

### Report માં શું રાખવું?

Title નો નમૂનો: **Daily Sanitation MIS — 9 October 2026 — Practice Only**.

સમયગાળો, Source, Wards, Collection/Segregation indicators, Waste અને Units, Pending complaints, Missing data, Exceptions, જવાબદાર વ્યક્તિ, Deadline અને Prepared/Reviewed વિગતો રાખો. અધિકારી માટે ટૂંકી Summary અને વિગતવાર પુરાવા અલગ રાખો.

નમૂના Action note: “10 ઓક્ટોબરના Practice data માં Ward 2 નું Coverage બીજા Wards કરતાં ઓછું છે. સેવા ન મળેલાં સ્થળો Field staff સાથે ચકાસીને કારણ નોંધવું.” માત્ર આંકડો જોઈને Vehicle failure થયું એવું ન માનો.

### Files અને પુરાવા ગોઠવવા

નામનો નમૂનો: `2026-10-09_Ward02_Collection_Reviewed_v1.xlsx`.

Raw, Working અને Reviewed versions અલગ રાખો. Evidence index માં Date, Ward, Activity, File reference, Source અને Review status રાખી શકો. Correction log માં જૂનું મૂલ્ય, સુધારેલું મૂલ્ય, કારણ, પુરાવો અને Reviewer રાખો.

અધિકૃત Storage અને Access વાપરો. Citizen records Public link અથવા Personal account પર ન મૂકો. જરૂરી હોય તેટલી જ Personal information રાખો. Save/Export પછી File ખુલે છે તે તપાસો અને Backup માંથી Restore પણ ચકાસો.

### Government portal ન વાપર્યો હોય તો શું કહેશો?

“આ ચોક્કસ Portal પર હજી કામ કર્યું નથી. Reporting માટે વ્યાખ્યા સમજવી, Data ચકાસવો, મંજૂરી લેવી, ધ્યાનથી Entry કરવી અને Acknowledgement સાચવવું જરૂરી છે તે સમજું છું. અધિકૃત Guidance અને દેખરેખ હેઠળ પ્રેક્ટિસ કરીને શીખીશ.”

અનુભવ ન હોય તો તેનો દાવો ન કરો. Public SBM pages અભ્યાસ માટે જુઓ; મંજૂરી વગર Municipal account માં પ્રવેશ ન કરો.

## Practical assignment — પહેલાં જાતે કરો

**9 ઓક્ટોબરની Rows 2–4 જ લો.** પહેલાં જવાબો ન વાંચો.

1. Households, Covered અને Segregating ના Totals કાઢો.
2. Overall coverage અને Covered ઘરોમાંથી Segregation % કાઢો.
3. Collected/Processed kg અને આ Exercise નો Processing share કાઢો.
4. સૌથી વધુ Complaints વાળો Ward અને તેની સંખ્યા શોધો.
5. અધિકારી માટે ત્રણ વાક્યની Summary અને એક Follow-up action લખો.

### Answer key

- Households **750**, Covered **675**, Segregating **515**.
- Coverage: **675/750 = 90%**.
- Segregation among covered: **515/675 ≈ 76.30%**.
- Collected **1800 kg**, Processed **1410 kg**.
- Processing share: **1410/1800 ≈ 78.33%** — આ Practice measure છે; Certified SBM indicator કે સાચી City performance નથી.
- Complaints કુલ **17**; Ward 2 માં સૌથી વધુ **8**.

બોલવાનો નમૂનો: “કાલ્પનિક 9 ઓક્ટોબરના Data માં 750 માંથી 675 ઘરોને સેવા મળી એટલે Coverage 90% છે. સેવા મળેલા ઘરોમાં Segregation 76.30% અને Collection ના 1800 kg માંથી 1410 kg Process થયેલ દર્શાવે છે. Ward 2 માં સૌથી વધુ આઠ ફરિયાદ હોવાથી તેમની વિગતો અને પુરાવા તપાસીને આગળની કાર્યવાહી નક્કી કરવી.”

હવે **10 ઓક્ટોબર** માટે જાતે કરો: Households **750**, Covered **680**, Segregating **525**, Collected **1810 kg**, Processed **1450 kg**, Complaints **15**. Coverage **90.67%**, Segregation **77.21%**, Processing share **80.11%**.

બંને તારીખનો Collected waste **3610 kg**, Processed **2860 kg**. Unique households **750**, **1500 નહીં**. બંને દિવસનું Household-day coverage ગણો તો **1355/1500 ≈ 90.33%**. Measure નું નામ સ્પષ્ટ આપો.

## આજના Interview પ્રશ્નો અને જવાબો

**9. કઈ Excel skills ઉપયોગી છે?** Sort/Filter, Totals, Conditional formulas, Lookup, Validation, PivotTable અને Charts. તમે જાતે કરી હોય તેવી એક Skill સમજાવો.

**10. SUMIF અને SUMIFS માં ફરક?** SUMIF એક શરત પ્રમાણે સરવાળો કરે; SUMIFS Ward અને Date જેવી એકથી વધુ શરત પણ લઈ શકે. Ranges સરખા હોવા જોઈએ.

**11. PivotTable કેમ વાપરો?** ઘણા Records માંથી Ward/Period પ્રમાણે ઝડપી Summary મળે. Data type, Sum/Count અને Filters તપાસું અને Data બદલાય તો Refresh કરું.

**12. Data validation શું છે?** Data જરૂરી Type અને Rule મુજબ છે કે નહીં તપાસવું. ઉદાહરણ: અધિકૃત Ward list અને સાચી Date. છતાં Source proof તપાસવો જરૂરી છે.

**13. Duplicate કેવી રીતે શોધો?** પહેલાં Unique key નક્કી કરું, Matching keys Flag કરું અને Source તપાસું. અલગ Date/Shift ની સમાન Ward rows Delete ન કરું.

**14. Missing અને Zero માં ફરક?** Zero એટલે ચકાસેલી સંખ્યા શૂન્ય છે. Missing એટલે માહિતી અજાણી/મળી નથી. તેને Pending બતાવી Record મંગાવું.

**15. Overall coverage કેવી રીતે ગણો?** એક જ સમયગાળા અને વિસ્તારના કુલ Covered / કુલ Eligible households. Ward size જુદા હોય તો તેમની % Average ખોટી થઈ શકે.

**16. Formula અણધાર્યું Zero આપે તો?** Criteria, Ranges, Date/Text, Spaces, Number types અને Filters તપાસું. નાના Example નો Manual answer સરખાવી પછી Report પર વિશ્વાસ કરું.

**17. Field અને Portal figures જુદા હોય તો?** Period, Scope, Units, Source અને Version સરખાવું. જવાબદાર Staff સાથે સ્પષ્ટતા કરી સુધારો નોંધું અને મંજૂર પ્રક્રિયાથી Update કરું.

## દિવસના અંતે ચકાસો

- [ ] SUMIF, SUMIFS અને Lookup સમજાવી શકું છું.
- [ ] PivotTable બનાવી અને Refresh કરી શકું છું.
- [ ] કુલ Numerator/Denominator થી Coverage ગણું છું.
- [ ] Missing, Zero અને Duplicate માં ફરક સમજું છું.
- [ ] Upload પહેલાં Check, Approval અને Evidence સમજાવી શકું છું.
- [ ] Assignment માં 750 Households, 675 Covered અને 90% Coverage આવ્યું છે.

બતાવી શકું તે Excel કામ:
મેં સુધારેલી ભૂલ:
મારો નબળો વિષય:

આગળ: [11 ઓક્ટોબર — IT અને Scenarios](./2026-10-11_Day_3_IT_and_Scenarios.md).

આ સામગ્રી [સંપૂર્ણ સંદર્ભ Guide](./Interview_Preparation_09_to_13_October_2026.md) પરથી ગોઠવેલી છે. સૂચવેલા વિષયો અને પ્રશ્નો તૈયારી માટે છે; આ અધિકૃત Interview syllabus નથી.
