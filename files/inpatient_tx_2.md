<table>
<thead>
<tr>
<th>Variable Name</th>
<th>Variable Type and Length (Bytes)</th>
<th>Values</th>
<th>Definition / Comments / Guideline</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr>
<td>PatID<sup>1</sup></td>
<td>Char (Site specific length)</td>
<td>Unique member identifier</td>
<td>Arbitrary person-level identifier. Used to link across tables.</td>
<td><code>123456789012345</code></td>
</tr>
<tr>
<td>EncounterID<sup>2</sup></td>
<td>Char (Site specific length)</td>
<td>Unique encounter identifier</td>
<td>Arbitrary encounter-level identifier. Used to link across the Encounter, Diagnosis, Procedure, Vital Signs, Inpatient Pharmacy, &amp; Inpatient Transfusion tables.</td>
<td><code>123456789012345_12242005_99218766_IP</code></td>
</tr>
<tr>
<td>TransID</td>
<td>Char (15)</td>
<td>Unique transfusion administration identifier</td>
<td>Retain b/c useful to map back to source data</td>
<td><code>123456789012345</code></td>
</tr>
<tr>
<td>TransCode</td>
<td>Char (15)</td>
<td>Code value for an infusion product</td>
<td>Must be paired with the correct TransCode_Type</td>
<td><code>123451224200599</code></td>
</tr>
<tr>
<td>TransCode_Type</td>
<td>Char(2)</td>
<td><code>CD</code> = CODABAR<br><code>IS</code> = ISBT</td>
<td>Transfusion product code type. This variable combined with the TransCode variable should be used to capture any type of Inpatient Infusion product in the source data. Other code types will be added as new terminologies are used.</td>
<td><code>CD</code></td>
</tr>
<tr>
<td>Orig_TransProd</td>
<td>Char (Site specific length)</td>
<td>Original product name/mneumonic</td>
<td>Name of product within Data Partner</td>
<td><code>Thawed POOLED PLATELETS</code></td>
</tr>
<tr>
<td>BloodType</td>
<td>Char(3)</td>
<td><code>A</code>, <code>B</code>, <code>O</code>, <code>AB</code> (upper case) with RH factor (<code>+</code>, <code>-</code>, or null only)</td>
<td>Blood type and Rh factors, left-justified. Convert any text Rh factor to symbols (e.g., &quot;pos&quot; to &quot;+&quot;, &quot;negative&quot; to &quot;-&quot;). Rh factor can be blank.</td>
<td><code>AB+</code></td>
</tr>
<tr>
<td>TDate_Start</td>
<td>Numeric (4)</td>
<td>SAS date value</td>
<td>Administration start date</td>
<td><code>12/1/2005</code></td>
</tr>
<tr>
<td>TTime_Start</td>
<td>Numeric (4)</td>
<td>SAS time value <code>HH:MM</code></td>
<td>Administration start time.</td>
<td><code>14:27</code></td>
</tr>
<tr>
<td>TDate_End</td>
<td>Numeric (4)</td>
<td>SAS date value</td>
<td>Administration end date</td>
<td><code>12/1/2005</code></td>
</tr>
<tr>
<td>TTime_End</td>
<td>Numeric (4)</td>
<td>SAS time value <code>HH:MM</code></td>
<td>Administration end time.</td>
<td><code>20:56</code></td>
</tr>
<tr>
<td rowspan=4>EncType</td>
<td rowspan=4>Char (2)</td>
<td><code>ED</code> = Emergency Department</td>
<td>Includes ED encounters that become inpatient stays (in which case inpatient stays would be a separate encounter). Excludes urgent care visits. ED claims should be pulled before hospitalization claims to ensure that ED with subsequent admission won't be rolled up in the hospital event.</td>
<td rowspan=4><code>IP</code></td>
</tr>
<tr>
<td><code>IP</code> = Inpatient Hospital Stay</td>
<td>Includes all inpatient stays, same-day hospital discharges, hospital transfers, and acute hospital care where the discharge is after the admission date.</td>
<td></td>
</tr>
<tr>
<td><code>IS</code> = Non-Acute Institutional Stay</td>
<td>Includes hospice, skilled nursing facility (SNF), rehab center, nursing home, residential, overnight non-hospital dialysis and other non-hospital stays.</td>
<td></td>
</tr>
<tr>
<td><code>OA</code> = Other Ambulatory Visit</td>
<td>Includes other non overnight AV encounters such as hospice visits, home health visits, skilled nursing facility visits, other non-hospital visits, as well as telemedicine, telephone and email consultations.</td>
</tr>
</tbody>
</table>