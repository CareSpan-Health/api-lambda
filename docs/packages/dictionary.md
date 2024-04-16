---
sidebar_position: 1
---

# Dictionary

## For Demographics

### Gender v1

| key | message |
| --- | ------- |
| 0   | Male    |
| 1   | Female  |
| 2   | Unknown |

```sql
-- Table: messages
-- Category: gender
SELECT `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'gender') AND (`lang` = 'en')
ORDER by `key`
```

### Gender Identity

| key | message                                               |
| --- | ----------------------------------------------------- |
| 0   | Male                                                  |
| 1   | Female                                                |
| 11  | Transgender male/Trans man/Female-to-male             |
| 12  | Transgender female/Trans woman/Male-to-female         |
| 13  | Genderqueer, neither exclusively male nor female      |
| 14  | Additional gender category/(or other), please specify |
| 15  | Choose not to disclose                                |

```sql
-- Table: messages
-- Category: genderidentity
SELECT `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'genderidentity') AND (`lang` = 'en')
ORDER by `key`
```

### Gender Orientation

| key | message                         |
| --- | ------------------------------- |
| 1   | Straight or heterosexual        |
| 2   | Lesbian, gay or homosexual      |
| 3   | Bisexual                        |
| 4   | Something else, please describe |
| 5   | Don’t know                      |
| 6   | Choose not to disclose          |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 34
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '34') AND (`language` = 'en')
ORDER by `key`
```

### Race

| key | message                                   |
| --- | ----------------------------------------- |
| 0   | White                                     |
| 1   | Black or African American                 |
| 2   | Asian                                     |
| 3   | Native Hawaiian or Other Pacific Islander |
| 4   | American Indian or Alaska Native          |
| 6   | Other                                     |
| 7   | Choose not to disclose                    |

```sql
-- Table: messages
-- Category: race
SELECT 
  `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'race') AND (`lang` = 'en')
ORDER BY `key`

```

### Ethnicity

| key | message                 |
| --- | ----------------------- |
| 0   | Not Hispanic or Latino  |
| 1   | Hispanic or Latino      |
| 3   | Spaniard                |
| 4   | Andalusian              |
| 5   | Asturian                |
| 6   | Castillian              |
| 7   | Catalonian              |
| 8   | Belearic Islander       |
| 9   | Gallego                 |
| 10  | Valencian               |
| 11  | Canarian                |
| 12  | Spanish Basque          |
| 13  | Mexican                 |
| 14  | Mexican American        |
| 15  | Mexicano                |
| 16  | Chicano                 |
| 17  | La Raza                 |
| 18  | Mexican American Indian |
| 19  | Central American        |
| 20  | Costa Rican             |
| 21  | Guatemalan              |
| 22  | Honduran                |
| 23  | Nicaraguan              |
| 24  | Panamanian              |
| 25  | Salvadoran              |
| 26  | Central American Indian |
| 27  | Canal Zone              |
| 28  | South American          |
| 29  | Argentinean             |
| 30  | Bolivian                |
| 31  | Chilean                 |
| 32  | Colombian               |
| 33  | Ecuadorian              |
| 34  | Paraguayan              |
| 35  | Peruvian                |
| 36  | Uruguayan               |
| 37  | Venezuelan              |
| 38  | South American Indian   |
| 39  | Criollo                 |
| 40  | Latin American          |
| 41  | Puerto Rican            |
| 42  | Cuban                   |
| 43  | Dominican               |
| 49  | Unknown                 |
| 50  | Choose not to disclose  |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 36
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '36') AND (`language` = 'en')
ORDER by `key`
```

### Marital

| key | message     |
| --- | ----------- |
| 0   | Single      |
| 1   | Married     |
| 2   | Divorced    |
| 3   | Widowed     |
| 4   | Partnership |
| 5   | Separated   |

```sql
-- Table: messages
-- Category: marital
SELECT 
  `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'marital') AND (`lang` = 'en')
ORDER BY `key`
```

### Religion

| key | message                                |
| --- | -------------------------------------- |
| 1   | Adventist                              |
| 2   | African Religions                      |
| 3   | Afro-Caribbean Religions               |
| 4   | Agnosticism                            |
| 5   | Anglican                               |
| 6   | Animism                                |
| 7   | Atheism                                |
| 8   | Babi & Baha'I faiths                   |
| 9   | Baptist                                |
| 10  | Bon                                    |
| 11  | Cao Dai                                |
| 12  | Celticism                              |
| 13  | Christian (non-Catholic, non-specific) |
| 14  | Confucianism                           |
| 15  | Cyberculture Religions                 |
| 16  | Divination                             |
| 17  | Fourth Way                             |
| 18  | Free Daism                             |
| 19  | Gnosis                                 |
| 20  | Hinduism                               |
| 21  | Humanism                               |
| 22  | Independent                            |
| 23  | Islam                                  |
| 24  | Jainism                                |
| 25  | Jehovah's Witnesses                    |
| 26  | Judaism                                |
| 27  | Latter Day Saints                      |
| 28  | Lutheran                               |
| 29  | Mahayana                               |
| 30  | Meditation                             |
| 31  | Messianic Judaism                      |
| 32  | Mitraism                               |
| 33  | New Age                                |
| 34  | non-Roman Catholic                     |
| 35  | Occult                                 |
| 36  | Orthodox                               |
| 37  | Paganism                               |
| 38  | Pentecostal                            |
| 39  | Process, The                           |
| 40  | Reformed/Presbyterian                  |
| 41  | Roman Catholic Church                  |
| 42  | Satanism                               |
| 43  | Scientology                            |
| 44  | Shamanism                              |
| 45  | Shiite (Islam)                         |
| 46  | Shinto                                 |
| 47  | Sikism                                 |
| 48  | Spiritualism                           |
| 49  | Sunni (Islam)                          |
| 50  | Taoism                                 |
| 51  | Theravada                              |
| 52  | Unitarian-Universalism                 |
| 53  | Universal Life Church                  |
| 54  | Vajrayana (Tibetan)                    |
| 55  | Veda                                   |
| 56  | Voodoo                                 |
| 57  | Wicca                                  |
| 58  | Yaohushua                              |
| 59  | Zen Buddhism                           |
| 60  | Zoroastrianism                         |
| 61  | Assembly of God                        |
| 62  | Brethren                               |
| 63  | Christian Scientist                    |
| 64  | Church of Christ                       |
| 65  | Church of God                          |
| 66  | Congregational                         |
| 67  | Disciples of Christ                    |
| 68  | Eastern Orthodox                       |
| 69  | Episcopalian                           |
| 70  | Evangelical Covenant                   |
| 71  | Friends                                |
| 72  | Full Gospel                            |
| 73  | Methodist                              |
| 74  | Native American                        |
| 75  | Nazarene                               |
| 76  | Presbyterian                           |
| 77  | Protestant                             |
| 78  | Protestant, No Denomination            |
| 79  | Reformed                               |
| 80  | Salvation Army                         |
| 81  | Unitarian Universalist                 |
| 82  | United Church of Christ                |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 35
SELECT 
  `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '35') AND (`language` = 'en')
ORDER by `key`
```

### Relationship Types v1

| key | message              |
| --- | -------------------- |
| 0   | Maternal Grandmother |
| 1   | Maternal Grandfather |
| 2   | Mother               |
| 3   | Father               |
| 4   | Sister               |
| 5   | Brother              |
| 6   | Child                |
| 7   | Other                |
| 8   | Paternal Grandfather |
| 9   | Paternal Grandmother |
| 10  | Aunt                 |
| 11  | Uncle                |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 27
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '27') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Relationship Types v2

| key | message                                             |
| --- | --------------------------------------------------- |
| 1   | Spouse                                              |
| 4   | Grandparent                                         |
| 5   | Grandson or Grandaughter                            |
| 7   | Nephew or Niece                                     |
| 10  | Foster Child                                        |
| 15  | Ward                                                |
| 17  | Stepson or Stepdaughter                             |
| 18  | Self                                                |
| 19  | Child                                               |
| 20  | Employee                                            |
| 21  | Unknown                                             |
| 22  | Handicapped Dependent                               |
| 23  | Sponsored Dependent                                 |
| 24  | Dependent of a Minor                                |
| 29  | Significant Other                                   |
| 32  | Mother                                              |
| 33  | Father                                              |
| 36  | Emancipated Minor                                   |
| 39  | Organ Donor                                         |
| 41  | Injured Plaintif                                    |
| 42  | Child Where Insured Has No Financial Responsibility |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 30
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '30') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

## For Health Record

### Smoker v1

| key | message                        |
| --- | ------------------------------ |
| 0   | Current every day smoker       |
| 1   | Current some day smoker        |
| 2   | Former smoker                  |
| 3   | Never smoker                   |
| 4   | Smoker, current status unknown |
| 5   | Unknown if ever smoked         |
| 6   | Current Heavy tobacco smoker   |
| 7   | Current Light tobacco smoker   |

```sql
-- Table: messages
-- Category: smoker
SELECT `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'smoker') AND (`lang` = 'en')
```

### Blood Type

| key | message |
| --- | ------- |
| 0   | O+      |
| 1   | O-      |
| 2   | A+      |
| 3   | A-      |
| 4   | B+      |
| 5   | B-      |
| 6   | AB+     |
| 7   | AB-     |

```sql
-- Table: messages
-- Category: bloodtype
SELECT 
  `ckey` as `key`, `message`
FROM `messages`
WHERE (`category` = 'bloodtype') AND (`lang` = 'en')
ORDER BY `key`
```

### Allergy Types

| key | message          |
| --- | ---------------- |
| 1   | Drug             |
| 2   | Food             |
| 3   | Insect           |
| 4   | Latex            |
| 5   | Mold             |
| 6   | Pet              |
| 7   | Pollen           |
| 8   | Skin             |
| 9   | Other            |
| 10  | No Known Allergy |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 25
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '25') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Allergy Reactions

| key | message              |
| --- | -------------------- |
| 1   | Abdominal Pain       |
| 2   | Anaphylactic Shock   |
| 3   | Constipation         |
| 4   | Diarrhea             |
| 5   | Difficulty Breathing |
| 6   | Dizziness            |
| 7   | Headache             |
| 8   | Itching              |
| 9   | Joint Pain           |
| 10  | Nausea/Vomiting      |
| 11  | Palpitations         |
| 12  | Rash/Hives           |
| 13  | Swelling             |
| 14  | Unknown              |
| 15  | Other                |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 68
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '68') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Allergy Severity

| key | message          |
| --- | ---------------- |
| 1   | Mild             |
| 2   | Moderate         |
| 3   | Serious          |
| 4   | Life Threatening |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 88
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '88') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Route

| key | snomed    | message                 |
| --- | --------- | ----------------------- |
| 1   | 6064005   | Topical route           |
| 2   | 10547007  | Auricular use           |
| 3   | 12130007  | Intra-articular route   |
| 4   | 16857009  | Vaginal use             |
| 5   | 26643006  | Oral use                |
| 6   | 34206005  | SC use                  |
| 7   | 37161004  | Rectal use              |
| 9   | 37839007  | Sublingual use          |
| 11  | 45890007  | Transdermal use         |
| 12  | 46713006  | Nasal use               |
| 13  | 47625008  | Intravenous use         |
| 14  | 54471007  | Buccal use              |
| 15  | 54485002  | Ophthalmic use          |
| 20  | 78421000  | Intramuscular use       |
| 25  | 372449004 | Dental use              |
| 26  | 372450004 | Endocervical use        |
| 50  | 404818005 | Intratracheal route     |
| 52  | 404820008 | Epidural route          |
| 137 | 447694001 | Respiratory tract route |

```sql
-- Table: ref_codes
-- type: route
SELECT `id` as `key`, `snomed`, `description` as message
FROM `ref_codes`
WHERE `type` = 'route' and `status` = 1
```

### Site

| key | snomed            | message                           |
| --- | ----------------- | --------------------------------- |
| 151 | 368209003         | Right upper arm structure         |
| 152 | 368208006         | Left upper arm structure          |
| 153 | 86367003          | Left upper quadrant of abdomen    |
| 154 | 50519007          | Right upper quadrant of abdomen   |
| 155 | 68505006          | Left lower quadrant of abdomen    |
| 156 | 48544008          | Right lower quadrant of abdomen   |
| 157 | 456271000124109   | Ventrogluteal region              |
| 158 | 72226001          | Rectus femoris structure          |
| 159 | 181681008         | Entire vastus lateralis muscle    |
| 160 | 16217701000119102 | Structure of left deltoid muscle  |
| 161 | 16217661000119109 | Structure of right deltoid muscle |
| 162 | 209570001         | Entire right thigh                |
| 163 | 209672000         | Entire left thigh                 |

```sql
-- Table: ref_codes
-- type: site
SELECT `id` as `key`, `snomed`, `description` as message
FROM `ref_codes`
WHERE `type` = 'site' and `status` = 1
```

### Medication Type

| key | message      |
| --- | ------------ |
| 1   | Long Term    |
| 2   | Supplements  |
| 3   | OTC          |
| 4   | Psychoactive |
| 5   | Other        |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 65
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '65') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Medication Statuses

#### For Self-Reporting

| key | message      |
| --- | ------------ |
| 1   | Active       |
| 2   | Inactive     |
| 3   | Discontinued |
| 4   | Deleted      |
| 5   | Completed    |

#### For Others, the following are added

| key | message          |
| --- | ---------------- |
| 6   | Cancel Requested |
| 7   | Cancel Pending   |
| 8   | Canceled         |
| 9   | Cancel Denied    |
| 10  | Changed          |
| 11  | Pending          |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 66
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '66') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Medication Discontinued Reasons

| key | message           |
| --- | ----------------- |
| 1   | Doctor Suggested  |
| 2   | Adverse Reactions |
| 3   | Allergy           |
| 4   | Can't Afford      |
| 5   | Completed Course  |
| 6   | Not Effective     |
| 7   | Ran Out           |
| 8   | Refused to Take   |
| 9   | Side Effects      |
| 10  | Wrong Dose        |
| 11  | Other             |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 67
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '67') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Prescription Statuses

| key | message          |
| --- | ---------------- |
| 1   | entered          |
| 2   | printed          |
| 3   | sending          |
| 4   | erxsent          |
| 5   | faxsent          |
| 6   | error            |
| 7   | deleted          |
| 8   | requested        |
| 9   | edited           |
| 10  | epcserror        |
| 11  | epcssigned       |
| 12  | readytosign      |
| 13  | pharmacyverified |

:::warning

Classification from **_DoseSpot_** (3rd Party)

:::

### Drug Classification

| key                                                    | message |
| ------------------------------------------------------ | ------- |
| `miscellaneous antipsychotic agents`                   | -       |
| `psychotherapeutic combinations`                       | -       |
| `phenothiazine antipsychotics`                         | -       |
| `psychotherapeutic agents`                             | -       |
| `antipsychotics`                                       | -       |
| `atypical antipsychotics`                              | -       |
| `Antipsychotic Agent Benzamide`                        | -       |
| `Antipsychotic Agent Benzisoxazole`                    | -       |
| `Antipsychotic Agent Benzothiazolylpiperazine`         | -       |
| `Antipsychotic Agent Benzylisothiazolylpiperazine`     | -       |
| `Antipsychotic Agent Butyrophenone`                    | -       |
| `Antipsychotic Agent Dibenzodiazepine`                 | -       |
| `Antipsychotic Agent Dibenzothiazepine`                | -       |
| `Antipsychotic Agent Dibenzoxazepine`                  | -       |
| `Antipsychotic Agent Dihydroindoline`                  | -       |
| `Antipsychotic Agent Diphenylbutylperidine`            | -       |
| `Antipsychotic Agent Phenothiazine Aliphatic`          | -       |
| `Antipsychotic Agent Phenothiazine Piperazine`         | -       |
| `Antipsychotic Agent Phenothiazine Piperidine`         | -       |
| `Antipsychotic Agent Thienobenzodiazepine`             | -       |
| `Antipsychotic Agent Thioxanthene Derivative`          | -       |
| `Antipsychotic Agent`                                  | -       |
| `Benzisoxazole (Antipsychotic)`                        | -       |
| `Butyrophenone Derivative (Antipsychotic)`             | -       |
| `Dibenzodiazepine (Antipsychotic)`                     | -       |
| `Dibenzoxazepine (Antipsychotic)`                      | -       |
| `Dihydroindoline (Antipsychotic)`                      | -       |
| `Psychostimulant`                                      | -       |
| `Antipsychotic Agent Quinolinone`                      | -       |
| `Second Generation (Atypical) Antipsychotic`           | -       |
| `First Generation (Typical) Antipsychotic`             | -       |
| `Antipsychotic Agent Typical Phenothiazine`            | -       |
| `Antipsychotic Agent Typical Phenothiazine Piperidine` | -       |

:::warning

Classification from **_DoseSpot_** (3rd Party)

:::

### Problem Status

| key | message      |
| --- | ------------ |
| 1   | Uncontrolled |
| 2   | Controlled   |
| 3   | Resolved     |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 41
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '41') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Immunization List

| key | message                                                                                                                          |
| --- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0   | Td (Tetanus)                                                                                                                     |
| 1   | Hepatitis A                                                                                                                      |
| 2   | Hepatitis B                                                                                                                      |
| 3   | Pneumonia                                                                                                                        |
| 4   | Influenza (FLU)                                                                                                                  |
| 5   | HPV (Human Papillomavirus)                                                                                                       |
| 6   | DTap                                                                                                                             |
| 7   | MMR (Measles, Mumps, and Rubella)                                                                                                |
| 8   | Varicella                                                                                                                        |
| 9   | Hib                                                                                                                              |
| 10  | Rotovirus                                                                                                                        |
| 11  | Polio                                                                                                                            |
| 12  | Prevnar                                                                                                                          |
| 13  | Adenovirus vaccine, type 4, live, oral                                                                                           |
| 14  | Adenovirus vaccine, type 7, live, oral                                                                                           |
| 15  | Adenovirus vaccine, unspecified formulation                                                                                      |
| 16  | Adenovirus, type 4 and type 7, live, oral                                                                                        |
| 17  | Anthrax immune globulin                                                                                                          |
| 18  | Anthrax vaccine                                                                                                                  |
| 19  | AS03 Adjuvant                                                                                                                    |
| 20  | Bacillus Calmette-Guerin vaccine                                                                                                 |
| 21  | Botulinum antitoxin                                                                                                              |
| 22  | Cholera vaccine, unspecified formulation                                                                                         |
| 23  | Cholera, BivWC                                                                                                                   |
| 24  | Cholera, live attenuated                                                                                                         |
| 25  | Cholera, WC-rBS                                                                                                                  |
| 26  | Cytomegalovirus immune globulin, intravenous                                                                                     |
| 27  | Diphtheria and Tetanus Toxoids and Acellular Pertussis Adsorbed, Inactivated Poliovirus, Haemophilus b Conjugate (Meningococcal  |
| 28  | Diphtheria and tetanus toxoids, adsorbed for pediatric use                                                                       |
| 29  | Diphtheria antitoxin                                                                                                             |
| 30  | Diphtheria, tetanus toxoids and acellular pertussis vaccine                                                                      |
| 31  | Diphtheria, tetanus toxoids and acellular pertussis vaccine, 5 pertussis antigens                                                |
| 32  | Diphtheria, tetanus toxoids and acellular pertussis vaccine, and poliovirus vaccine, inactivated                                 |
| 33  | Diphtheria, tetanus toxoids and acellular pertussis vaccine, Haemophilus influenzae type b conjugate, and poliovirus vaccine, in |
| 34  | Diphtheria, tetanus toxoids and pertussis vaccine                                                                                |
| 35  | DTaP-Haemophilus influenzae type b conjugate vaccine                                                                             |
| 36  | DTaP-hepatitis B and poliovirus vaccine                                                                                          |
| 37  | DTP- Haemophilus influenzae type b conjugate and hepatitis b vaccine                                                             |
| 38  | DTP-Haemophilus influenzae type b conjugate vaccine                                                                              |
| 39  | Haemophilus influenzae type b conjugate and Hepatitis B vaccine                                                                  |
| 40  | Haemophilus influenzae type b vaccine, HbOC conjugate                                                                            |
| 41  | Haemophilus influenzae type b vaccine, PRP-D conjugate                                                                           |
| 42  | Haemophilus influenzae type b vaccine, PRP-OMP conjugate                                                                         |
| 43  | Haemophilus influenzae type b vaccine, PRP-T conjugate                                                                           |
| 44  | Hep A, live attenuated-IM                                                                                                        |
| 45  | Hepatitis A and hepatitis B vaccine                                                                                              |
| 46  | Hepatitis A vaccine, adult dosage                                                                                                |
| 47  | Hepatitis A vaccine, pediatric dosage, unspecified formulation                                                                   |
| 48  | Hepatitis A vaccine, pediatric/adolescent dosage, 2 dose schedule                                                                |
| 49  | Hepatitis A vaccine, pediatric/adolescent dosage, 3 dose schedule                                                                |
| 50  | Hepatitis B immune globulin                                                                                                      |
| 51  | Hepatitis B vaccine (recombinant), CpG adjuvanted                                                                                |
| 52  | Hepatitis B vaccine, adolescent/high risk infant dosage                                                                          |
| 53  | Hepatitis B vaccine, adult dosage                                                                                                |
| 54  | Hepatitis B vaccine, dialysis patient dosage                                                                                     |
| 55  | Hepatitis B vaccine, pediatric or pediatric/adolescent dosage                                                                    |
| 56  | Historical diphtheria and tetanus toxoids and acellular pertussis, poliovirus, Haemophilus b conjugate and hepatitis B (recombin |
| 57  | Historical record of a typhus vaccination                                                                                        |
| 58  | Human papilloma virus vaccine, bivalent                                                                                          |
| 59  | Human papilloma virus vaccine, quadrivalent                                                                                      |
| 60  | Human Papillomavirus 9-valent vaccine                                                                                            |
| 61  | Human rabies vaccine from Chicken fibroblast culture                                                                             |
| 62  | Human Rabies vaccine from human diploid cell culture                                                                             |
| 63  | Immune globulin, intramuscular                                                                                                   |
| 64  | Immune globulin, intravenous                                                                                                     |
| 65  | Immune globulin, unspecified formulation                                                                                         |
| 66  | Influenza A monovalent (H5N1), adjuvanted, National stockpile 2013                                                               |
| 67  | Influenza nasal, unspecified formulation                                                                                         |
| 68  | Influenza virus vaccine, H5N1, A/Vietnam/1203/2004 (national stockpile)                                                          |
| 69  | Influenza virus vaccine, live, attenuated, for intranasal use                                                                    |
| 70  | Influenza virus vaccine, split virus (incl. purified surface antigen)-retired CODE                                               |
| 71  | Influenza virus vaccine, whole virus                                                                                             |
| 72  | Influenza, high dose seasonal, preservative-free                                                                                 |
| 73  | Influenza, injectable, Madin Darby Canine Kidney, quadrivalent with preservative                                                 |
| 74  | Influenza, injectable, Madin Darby Canine Kidney, preservative free                                                              |
| 75  | Influenza, injectable, Madin Darby Canine Kidney, preservative free, quadrivalent                                                |
| 76  | Influenza, injectable, quadrivalent, contains preservative                                                                       |
| 77  | Influenza, injectable, quadrivalent, preservative free                                                                           |
| 78  | Influenza, injectable,quadrivalent, preservative free, pediatric                                                                 |
| 79  | Influenza, intradermal, quadrivalent, preservative free, injectable                                                              |
| 80  | Influenza, live, intranasal, quadrivalent                                                                                        |
| 81  | Influenza, seasonal, injectable                                                                                                  |
| 82  | Influenza, seasonal, injectable, preservative free                                                                               |
| 83  | Japanese Encephalitis vaccine for intramuscular administration                                                                   |
| 84  | Japanese Encephalitis Vaccine SC                                                                                                 |
| 85  | Japanese Encephalitis vaccine, unspecified formulation                                                                           |
| 86  | Lyme disease vaccine                                                                                                             |
| 87  | Measles and rubella virus vaccine                                                                                                |
| 88  | Measles virus vaccine                                                                                                            |
| 89  | Measles, mumps, rubella, and varicella virus vaccine                                                                             |
| 90  | Meningococcal ACWY vaccine, unspecified formulation                                                                              |
| 91  | Meningococcal B vaccine, fully recombinant                                                                                       |
| 92  | Meningococcal B vaccine, recombinant, OMV, adjuvanted                                                                            |
| 93  | Meningococcal B, unspecified formulation                                                                                         |
| 94  | Meningococcal C conjugate vaccine                                                                                                |
| 95  | Meningococcal Groups C and Y and Haemophilus b Tetanus Toxoid Conjugate Vaccine                                                  |
| 96  | Meningococcal oligosaccharide (groups A, C, Y and W-135) diphtheria toxoid conjugate vaccine (MCV4O)                             |
| 97  | Meningococcal polysaccharide (groups A, C, Y and W-135) diphtheria toxoid conjugate vaccine (MCV4P)                              |
| 98  | Meningococcal polysaccharide vaccine (MPSV4)                                                                                     |
| 99  | Meningococcal vaccine of unknown formulation and unknown serogroups                                                              |
| 100 | Meningococcal, MCV4, unspecified conjugate formulation(groups A, C, Y and W-135)                                                 |
| 101 | Mumps virus vaccine                                                                                                              |
| 102 | No vaccine administered                                                                                                          |
| 103 | Non-US bivalent oral polio vaccine (types 1 and 3)                                                                               |
| 104 | Non-US diphtheria, tetanus toxoids and acellular pertussis vaccine, Haemophilus influenzae type b conjugate, and poliovirus vacc |
| 105 | Non-US monovalent oral polio vaccine, unspecified formulation                                                                    |
| 106 | Novel influenza-H1N1-09, all formulations                                                                                        |
| 107 | Novel influenza-H1N1-09, injectable                                                                                              |
| 108 | Novel Influenza-H1N1-09, live virus for nasal administration                                                                     |
| 109 | Novel influenza-H1N1-09, preservative-free, injectable                                                                           |
| 110 | Oral Polio Vaccine, Unspecified formulation                                                                                      |
| 111 | Parainfluenza-3 virus vaccine                                                                                                    |
| 112 | Pertussis vaccine                                                                                                                |
| 113 | Plague vaccine                                                                                                                   |
| 114 | Pneumococcal conjugate vaccine, 10 valent                                                                                        |
| 115 | Pneumococcal conjugate vaccine, 7 valent                                                                                         |
| 116 | Pneumococcal Conjugate, unspecified formulation                                                                                  |
| 117 | Pneumococcal polysaccharide vaccine, 23 valent                                                                                   |
| 118 | Poliovirus vaccine, inactivated                                                                                                  |
| 119 | Rabies immune globulin                                                                                                           |
| 120 | Rabies vaccine, for intradermal injection                                                                                        |
| 121 | Rabies vaccine, for intramuscular injection RETIRED CODE                                                                         |
| 122 | Rabies vaccine, unspecified formulation                                                                                          |
| 123 | Respiratory syncytial virus immune globulin, intravenous                                                                         |
| 124 | Respiratory syncytial virus monoclonal antibody (palivizumab), intramuscular                                                     |
| 125 | Rho(D) Immune globulin - IM                                                                                                      |
| 126 | Rho(D) Immune globulin- IV or IM                                                                                                 |
| 127 | Rho(D) Unspecified formulation                                                                                                   |
| 128 | Rotavirus, live, monovalent vaccine                                                                                              |
| 129 | Rotavirus, live, pentavalent vaccine                                                                                             |
| 130 | Rotavirus, live, tetravalent vaccine                                                                                             |
| 131 | Rubella and mumps virus vaccine                                                                                                  |
| 132 | Rubella virus vaccine                                                                                                            |
| 133 | Seasonal influenza, intradermal, preservative free                                                                               |
| 134 | Seasonal trivalent influenza vaccine, adjuvanted, preservative free                                                              |
| 135 | Seasonal, quadrivalent, recombinant, injectable influenza vaccine, preservative free                                             |
| 136 | Seasonal, trivalent, recombinant, injectable influenza vaccine, preservative free                                                |
| 137 | Staphylococcus bacteriophage lysate                                                                                              |
| 138 | Tetanus and diphtheria toxoids, adsorbed, preservative free, for adult use (2 Lf of tetanus toxoid and 2 Lf of diphtheria toxoid |
| 139 | Tetanus and diphtheria toxoids, adsorbed, preservative free, for adult use (5 Lf of tetanus toxoid and 2 Lf of diphtheria toxoid |
| 140 | Tetanus and diphtheria toxoids, not adsorbed, for adult use                                                                      |
| 141 | Tetanus immune globulin                                                                                                          |
| 142 | Tetanus immune globulin                                                                                                          |
| 143 | Tetanus toxoid, adsorbed                                                                                                         |
| 144 | Tetanus toxoid, not adsorbed                                                                                                     |
| 145 | Tetanus toxoid, reduced diphtheria toxoid, and acellular pertussis vaccine, adsorbed                                             |
| 146 | Tetanus toxoid, unspecified formulation                                                                                          |
| 147 | Tick-borne encephalitis vaccine                                                                                                  |
| 148 | Trivalent poliovirus vaccine, live, oral                                                                                         |
| 149 | Tuberculin skin test; old tuberculin, multipuncture device                                                                       |
| 150 | Tuberculin skin test; purified protein derivative solution, intradermal                                                          |
| 151 | Tuberculin skin test; purified protein derivative, multipuncture device                                                          |
| 152 | Tuberculin skin test; unspecified formulation                                                                                    |
| 153 | Tularemia vaccine                                                                                                                |
| 154 | Typhoid vaccine, live, oral                                                                                                      |
| 155 | Typhoid vaccine, parenteral, acetone-killed, dried (U.S. military)                                                               |
| 156 | Typhoid vaccine, parenteral, other than acetone-killed, dried                                                                    |
| 157 | Typhoid vaccine, unspecified formulation                                                                                         |
| 158 | Typhoid Vi capsular polysaccharide vaccine                                                                                       |
| 159 | Vaccinia (smallpox) vaccine                                                                                                      |
| 160 | Vaccinia (smallpox) vaccine, diluted                                                                                             |
| 161 | Vaccinia immune globulin                                                                                                         |
| 162 | Varicella zoster immune globulin                                                                                                 |
| 163 | Venezuelan equine encephalitis vaccine, unspecified formulation                                                                  |
| 164 | Venezuelan equine encephalitis, inactivated                                                                                      |
| 165 | Venezuelan equine encephalitis, live, attenuated                                                                                 |
| 166 | Yellow fever vaccine                                                                                                             |
| 167 | Yellow fever vaccine alternative formulation                                                                                     |
| 168 | Yellow fever vaccine, unspecified formulation                                                                                    |
| 169 | Zoster vaccine recombinant                                                                                                       |
| 170 | Zoster vaccine, live                                                                                                             |
| 171 | Zoster vaccine, unspecified formulation                                                                                          |
| 172 | Pfizer COVID-19 Vaccine                                                                                                          |
| 173 | Moderna COVID-19 Vaccine                                                                                                         |
| 174 | AstraZeneca COVID-19 Vaccine                                                                                                     |
| 175 | Janssen COVID-19 Vaccine                                                                                                         |
| 176 | Novavax COVID-19 Vaccine                                                                                                         |
| 177 | TDAP                                                                                                                             |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 4
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '4') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Immunization Status

| key | message   |
| --- | --------- |
| 1   | Completed |
| 2   | Not Done  |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 95
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '95') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Immunization Rejects

| key | message                   |
| --- | ------------------------- |
| 1   | Immunity                  |
| 2   | Medical precaution        |
| 3   | Out of stock              |
| 4   | Patient Objection         |
| 5   | philosophical Objection   |
| 6   | Religious Objection       |
| 7   | Vaccine Efficacy Concerns |
| 8   | Vaccine Safety Concerns   |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 98
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '98') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

## For Orders

### Lab Order Types

| key | message                          |
| --- | -------------------------------- |
| 1   | Organ or Disease Panels          |
| 2   | Hematology                       |
| 3   | Alphabetical / Combination Tests |
| 4   | Microbiology                     |

```sql
-- Table: ref_order_types
-- categories_id: 18
SELECT `order_type_index` as `key`, `order_type` as `message`
FROM `ref_order_types` WHERE `categories_id` = '18'
AND `status` = 1
```

### Lab Order Tests

| type_key | test_key | message                                       |
| -------- | -------- | --------------------------------------------- |
| 1        | 0        | Acute Hepatitis Panel                         |
| 1        | 1        | Basic Metabolic Panel (8)                     |
| 1        | 2        | Comp Metabolic Panel (14)                     |
| 1        | 3        | Electrolyte Panel                             |
| 1        | 4        | Hepatic Function Panel (7)                    |
| 1        | 5        | Lipid Panel                                   |
| 1        | 6        | Lipid Panel w/LDL/HDL Ratio                   |
| 1        | 7        | Lipid Panel w/TC-HDL Ratio                    |
| 1        | 8        | Lipid Panel w/Non-HDL Cholesterol             |
| 1        | 9        | Lipid Cascade                                 |
| 1        | 10       | Lipid Cascade with Rfx to ApoB                |
| 1        | 11       | Renal Function Panel                          |
| 1        | 12       | Other                                         |
| 2        | 0        | CBC w Diff & Pit                              |
| 2        | 1        | CBC wo Diff w Pit                             |
| 2        | 2        | Hematocrit                                    |
| 2        | 3        | Hemoglobin                                    |
| 2        | 4        | Platelet Count                                |
| 2        | 5        | RBC Count                                     |
| 2        | 6        | WBC Count                                     |
| 2        | 7        | Differential/Total WBC Count                  |
| 2        | 8        | Other                                         |
| 3        | 0        | ABO and Rh                                    |
| 3        | 1        | Albumin                                       |
| 3        | 2        | Alkaline Phosphatase                          |
| 3        | 3        | ALT (SGPT)                                    |
| 3        | 4        | Amylase                                       |
| 3        | 5        | Antinuclear Antibodies                        |
| 3        | 6        | AST (SGOT)                                    |
| 3        | 7        | B12 and Folate                                |
| 3        | 8        | Bilirubin, Total                              |
| 3        | 9        | BUN                                           |
| 3        | 10       | Calcium                                       |
| 3        | 11       | C-Reactive Protein (CRP), Quant               |
| 3        | 12       | hsCardiac C-Reactive Protein (CRP)            |
| 3        | 13       | Carbamazepine (Tegretol)                      |
| 3        | 14       | CEA                                           |
| 3        | 15       | Cholesterol, Total                            |
| 3        | 16       | Creatinine                                    |
| 3        | 17       | Digoxin (Lanoxin)                             |
| 3        | 18       | Estradiol                                     |
| 3        | 19       | Ferritin                                      |
| 3        | 20       | FSD and LH                                    |
| 3        | 21       | GGT                                           |
| 3        | 22       | Glucose, Plasma                               |
| 3        | 23       | Glucose, Serum                                |
| 3        | 24       | hCG, Beta Subunit, Qual (Serum Pregnancy)     |
| 3        | 25       | hCG, Beta Subunit, Quant                      |
| 3        | 26       | HDL Cholesterol                               |
| 3        | 27       | Hgb A1C                                       |
| 3        | 28       | Hep A Antibody, lgM                           |
| 3        | 29       | Hep B Surface Antibody                        |
| 3        | 30       | Hep B Surface Antigen                         |
| 3        | 31       | HCV Ab w/Rfx to Ab Verification               |
| 3        | 32       | HIV - 1/0/2 Antibodies                        |
| 3        | 33       | H pylori Urea Breath                          |
| 3        | 34       | H pylori Stool Antigen                        |
| 3        | 35       | Iron and IBC                                  |
| 3        | 36       | LDH                                           |
| 3        | 37       | Lithium (Eskalith)                            |
| 3        | 38       | Magnesium                                     |
| 3        | 39       | Mononucleosis Test, Qual                      |
| 3        | 40       | NMR LipoProfile                               |
| 3        | 41       | Phenobarbital (Luminal)                       |
| 3        | 42       | Phenytoin (Dilantin)                          |
| 3        | 43       | Phosphorus                                    |
| 3        | 44       | Potassium                                     |
| 3        | 45       | Prolactin                                     |
| 3        | 46       | PSA                                           |
| 3        | 47       | PSA, Free: Total Ratio                        |
| 3        | 48       | Prothrombin time (PT)/INR                     |
| 3        | 49       | PT and PTT Activated                          |
| 3        | 50       | PTT Activated                                 |
| 3        | 51       | Rheumatoid Arthritis Factor                   |
| 3        | 52       | RPR                                           |
| 3        | 53       | Rubella Antibodies, IgG                       |
| 3        | 54       | Sed Rate, Westergren                          |
| 3        | 55       | Sodium                                        |
| 3        | 56       | Testosterone, Total                           |
| 3        | 57       | Testosterone, Women/Children                  |
| 3        | 58       | Theophylline                                  |
| 3        | 59       | Thyroid Cascade Profile                       |
| 3        | 60       | Thyroxine (T4)                                |
| 3        | 61       | Thyroxine (T4) Free                           |
| 3        | 62       | T.pallidum Screening Cascade                  |
| 3        | 63       | Triglycerides                                 |
| 3        | 64       | Triiodothyronine (T3)                         |
| 3        | 65       | T3Uptake                                      |
| 3        | 66       | TSH, 3rd generation                           |
| 3        | 67       | Uric Acid                                     |
| 3        | 68       | Urinalysis                                    |
| 3        | 69       | Vitamin D, 25-Hydroxy                         |
| 3        | 70       | Lyme                                          |
| 3        | 71       | Other                                         |
| 3        | 73       | VDRL, Cerebrospinal Fluid                     |
| 3        | 74       | HSV Type 1, IgG                               |
| 3        | 75       | HSV Type 2, IgG                               |
| 4        | 0        | Aerobic Bacterial Culture                     |
| 4        | 1        | Fungus Culture                                |
| 4        | 2        | Genital Culture, Routine                      |
| 4        | 3        | Gram Stain                                    |
| 4        | 4        | Grp B Strep Detect, NAA                       |
| 4        | 5        | Grp B Strep Detect, NAA Rfx to suscept        |
| 4        | 6        | Lower Respiratory Culture                     |
| 4        | 7        | Occult Blood, Fecal, iA                       |
| 4        | 8        | Ova and Parasites                             |
| 4        | 9        | Stool Culture                                 |
| 4        | 10       | Throat Beta-Hemolytic Strep Cult, Group A     |
| 4        | 11       | Upper Respiratory Culture, Routine            |
| 4        | 12       | Urine Culture, Routine                        |
| 4        | 13       | Other                                         |
| 4        | 15       | Chlamydia Trachomatis Culture                 |
| 4        | 18       | Chlamydia Trachomatis, NAA                    |
| 4        | 16       | Neisseria Gonorrhoeae Culture Only            |
| 4        | 19       | Neisseria Gonorrhoeae, NAA                    |
| 4        | 17       | Herpes Simplex Virus (HSV) Culture and Typing |
| 5        | 0        | NuSwab Vaginitis (VG)                         |
| 5        | 1        | NuSwab Vaginitis Plus (VG+)                   |
| 5        | 2        | Bacterial Vaginosis, NAA                      |
| 5        | 3        | C. albicans & C. glabrata, NAA                |
| 5        | 4        | Candida Six-species Profile                   |
| 5        | 5        | Chlamydia/Gonoccoccus, NAA                    |
| 5        | 6        | Ct/Ng/Tv                                      |
| 5        | 7        | Genital Mycoplasmas, Swab                     |
| 5        | 8        | HSV 1 & 2, NAA                                |
| 5        | 9        | Trichomonas vaginalis, NAA                    |
| 5        | 10       | Other                                         |
| 6        | 0        | Chronic Kidney Disease Report                 |
| 6        | 1        | Cardiovascular Risk Assessment Report         |
| 6        | 2        | Other                                         |

```sql
-- Table: order_tests
-- categories_id: 18

SELECT 
-- test.`order_test_index`, 
test.`order_type_index` as `type_key`, test.`order_test_key` as `test_key`, test.`label` as `message`
-- test.`parent_table`, test.`parent_id` as `parent_test_key`
FROM `order_tests` test, `ref_order_types` t
WHERE (test.`language` = 'en') AND (test.`status` = '1')
AND t.`categories_id` = 18 AND test.`order_type_index` = t.`order_type_index`
AND test.`parent_table` is null

```

### In House Tests

:::note

Subject to change as this is configurable

:::

| key | message                                                                                                       |
| --- | ------------------------------------------------------------------------------------------------------------- |
| 1   | Manual urinalysis using tablet reagent                                                                        |
| 2   | Urine pregnancy test using visual color comparison method                                                     |
| 3   | Qualitative analysis of occult blood in feces by peroxidase activity                                          |
| 4   | Measurement of glucose in blood using reagent strip                                                           |
| 6   | Intradermal tuberculosis skin test                                                                            |
| 7   | Influenza virus detection by nucleic acid using multiplex reverse transcription and amplified probe technique |
| 8   | Respiratory virus detection by nucleic acid using amplified probe technique                                   |
| 9   | Group A Streptococcus detection by nucleic acid using amplified probe technique                               |
| 10  | Influenza antigen detection by immunoassay with direct optical observation                                    |
| 11  | Hgb A1C                                                                                                       |
| 12  | Urine drug tests: Drug test(s), presumptive, any number of drug classes, qualitative                          |
| 13  | Urinalysis macro (dipstick) panel                                                                             |
| 14  | SARS-CoV-2 (COVID-19) Ag [Presence] in Respiratory specimen by Rapid immunoassay                              |
| 15  | Drugs of abuse panel - Urine by Screen method                                                                 |

```sql
-- Table: ref_inhouse_labs

SELECT 
`inhouse_labs_id` as `key`, 
-- `client_id`, `cptcode`, `code_type`, `loinc`, 
`lab` as `message`
-- , `can_enter_results`, `active`
FROM `ref_inhouse_labs`
WHERE `active` = 1
```

### Imaging Order Types

| key | message          |
| --- | ---------------- |
| 7   | MRI              |
| 8   | CT               |
| 9   | X-Ray            |
| 10  | Fluoroscopy      |
| 11  | Ultrasound       |
| 12  | Nuclear Medicine |
| 13  | Breast Imaging   |
| 14  | DEXA             |

```sql
-- Table: ref_order_types
-- categories_id: 19
SELECT `order_type_index` as `key`, `order_type` as `message`
FROM `ref_order_types` WHERE `categories_id` = '19'
AND `status` = 1
```

### Imaging Order Tests

| type_key | test_key | message                                 |
| -------- | -------- | --------------------------------------- |
| 7        | 3        | Brain MRI                               |
| 7        | 4        | Brain MRA                               |
| 7        | 5        | Cervical Spine                          |
| 7        | 6        | Thoracic Spine                          |
| 7        | 7        | Lumbar Spine                            |
| 7        | 8        | Knee                                    |
| 7        | 11       | Shoulder                                |
| 7        | 14       | Extremity Other                         |
| 8        | 3        | Head CT                                 |
| 8        | 4        | Sinus                                   |
| 8        | 5        | Cervical Spine                          |
| 8        | 6        | Thoracic Spine                          |
| 8        | 7        | Lumbar spine                            |
| 8        | 8        | CTA                                     |
| 8        | 10       | Abdomen and Pelvis                      |
| 8        | 11       | Abdomen                                 |
| 8        | 12       | Pelvis                                  |
| 8        | 13       | Renal Colic                             |
| 8        | 14       | Urogram                                 |
| 8        | 15       | Cardiac                                 |
| 8        | 16       | With Calcium Score                      |
| 8        | 17       | Extremity                               |
| 8        | 19       | Other                                   |
| 8        | 21       | Chest CT                                |
| 9        | 0        | Chest (PA/Lateral)                      |
| 9        | 1        | Chest (1 view)                          |
| 9        | 2        | Acute abdomen (2 view abd + 1 view cxr) |
| 9        | 3        | KUB                                     |
| 9        | 4        | Cervical Spine                          |
| 9        | 5        | Thoracic Spine                          |
| 9        | 6        | Lumbar Spine                            |
| 9        | 8        | Extremity/Joint                         |
| 9        | 10       | Other                                   |
| 10       | 0        | Esophagram                              |
| 10       | 1        | Upper GI                                |
| 10       | 2        | Small bowel follow-through              |
| 10       | 3        | Video swallowing study                  |
| 10       | 4        | Barium enema                            |
| 10       | 6        | VCUG                                    |
| 10       | 7        | Cervical Myelogram                      |
| 10       | 8        | Thoracic Myelogram                      |
| 10       | 9        | Lumbar Myelogram                        |
| 10       | 10       | Lumbar puncture                         |
| 10       | 16       | Other                                   |
| 11       | 0        | Complete abdomen                        |
| 11       | 1        | Limited abdomen                         |
| 11       | 3        | Pelvis                                  |
| 11       | 4        | OB                                      |
| 11       | 5        | Renal                                   |
| 11       | 6        | Scrotum                                 |
| 11       | 7        | Thyroid                                 |
| 11       | 8        | Thyroid FNA                             |
| 11       | 9        | Carotid                                 |
| 11       | 10       | AAA                                     |
| 11       | 11       | Venous (DVT) Lower extremity            |
| 11       | 15       | Venous (DVT) Upper extremity            |
| 11       | 19       | Arterial                                |
| 11       | 22       | Full Peripheral Lower extremity         |
| 11       | 26       | Full Peripheral Upper extremity         |
| 11       | 30       | Other                                   |
| 12       | 0        | Whole body bone scan                    |
| 12       | 3        | 3 phase bone scan                       |
| 12       | 6        | Multiple areas bone scan                |
| 12       | 9        | Thyroid uptake + scan                   |
| 12       | 10       | MUGA                                    |
| 12       | 11       | Gastric emptying                        |
| 12       | 15       | HIDA                                    |
| 12       | 17       | Renal scan                              |
| 12       | 21       | Myocardial perfusion                    |
| 12       | 24       | PET/CT                                  |
| 12       | 26       | Other                                   |
| 13       | 0        | Screening mammogram                     |
| 13       | 1        | Breast ultrasound                       |
| 13       | 2        | Diagnostic mammogram                    |
| 13       | 3        | Breast MRI                              |
| 13       | 4        | Other                                   |
| 14       | 0        | Hip/lumbar                              |
| 14       | 1        | Forearm/ankle                           |

```sql
-- Table: order_tests
-- categories_id: 19

SELECT 
-- test.`order_test_index`, 
test.`order_type_index` as `type_key`, test.`order_test_key` as `test_key`, test.`label` as `message`
-- test.`parent_table`, test.`parent_id` as `parent_test_key`
FROM `order_tests` test, `ref_order_types` t
WHERE (test.`language` = 'en') AND (test.`status` = '1')
AND t.`categories_id` = 19 AND test.`order_type_index` = t.`order_type_index`
AND test.`parent_table` is null

```

## For Assessments (Evaluations/Questionnaires)

### Assessments

| key | type | name                                                             |
| --- | ---- | ---------------------------------------------------------------- |
| 2   | 0    | Patient Health Questionnaire (PHQ-9)                             |
| 3   | 0    | Generalized Anxiety Disorder Assessment (GAD-7)                  |
| 5   | 1    | COVID-19 Screening-and-Response Program V3                       |
| 6   | 0    | Geriatric depression scale (GDS)                                 |
| 7   | 0    | Epworth Sleepiness Scale                                         |
| 8   | 0    | Mood Disorder Questionnaire                                      |
| 9   | 0    | MINI Modernized                                                  |
| 10  | 0    | Mini Health Survey                                               |
| 11  | 0    | Zung Self-Rating Depression Scale                                |
| 12  | 0    | CAGE Questionnaire                                               |
| 13  | 0    | Adult ADHD Self-Report Scale (ASRS-v1.1)                         |
| 15  | 3    | Patient Health Questionnaire (PHQ-2)                             |
| 16  | 4    | Humiliation, Afraid, Rape, and Kick Questionnaire [HARK]         |
| 17  | 5    | Alcohol Use Disorder Identification Test C (AUDIT-C)             |
| 19  | 5    | DSM-5 Self-Rated Level 1 Cross-Cutting Symptom Measure - Adult   |
| 23  | 4    | Social Connection Isolation Panel                                |
| 26  | 3    | Pandemic Effects                                                 |
| 27  | 8    | Pediatric Symptom Checklist                                      |
| 28  | 1    | Screening Checklist for Contraindications to Vaccines for Adults |
| 29  | 1    | Screening Questionnaire for Child and Teen Immunization          |
| 30  | 8    | Screen for Child Anxiety Related Disorders - Parent              |
| 31  | 8    | Screen for Child Anxiety Related Disorders - Child               |
| 32  | 8    | SAD PERSONS                                                      |
| 33  | 8    | SAD PERSONS - Modified                                           |
| 34  | 8    | CRIES-13 Parent Version                                          |
| 35  | 8    | CRIES-8 Revised Child Impact of Events Scale                     |
| 36  | 8    | CRAFFT Questionnaire                                             |
| 37  | 8    | Center for Epidemiologic Studies Depression Scale (CES-D)        |
| 38  | 5    | Clinical Opiate Withdrawal Scale (COWS)                          |
| 7   | 0    | Epworth-Schläfrigkeitsskala (ESS)                                |

```sql
-- Table: ref_assessments

SELECT 
    `assessments_key` as `key`,
    `type`, 
    `name`
FROM `ref_assessments`
WHERE `active` = 1

```

### Assessment Type

| key | message            |
| --- | ------------------ |
| 0   | Behavioral         |
| 1   | Screening          |
| 2   | UrgentCare         |
| 3   | Psychosocial       |
| 4   | General            |
| 5   | Tobacco/Alcohol    |
| 6   | Safety             |
| 7   | Religious/Cultural |
| 8   | Pediatric          |
| 9   | Dosha - Vikruti    |
| 10  | Intake             |
| 11  | Dosha - Prakruti   |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 23
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '23') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Assessment Answer Statuses

| key | message            |
| --- | ------------------ |
| 1   | Unknown            |
| 2   | Declines to Answer |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 81
-- dictionary_type: Assessment Answer Statuses
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '81') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

## For Review of Systems

### Review of Systems

| type | key | label                             |
| ---- | --- | --------------------------------- |
| 1    | 0   | Chills/Sweats                     |
| 1    | 1   | Fatigue                           |
| 1    | 2   | Fever                             |
| 1    | 3   | Feeling Unwell                    |
| 1    | 4   | Weight Gain/Loss                  |
| 1    | 99  | Other                             |
| 2    | 0   | Cough                             |
| 2    | 1   | TB Exposure                       |
| 2    | 2   | Shortness of Breath               |
| 2    | 3   | Wheezing                          |
| 2    | 99  | Other                             |
| 3    | 0   | Anxiety/Restlessness              |
| 3    | 1   | Depression                        |
| 3    | 2   | Insomnia                          |
| 3    | 3   | Trouble Concentrating/Confusion   |
| 3    | 4   | Hopelessness                      |
| 3    | 5   | Change in Alcohol/Drug Use        |
| 3    | 6   | Hallucinations                    |
| 3    | 7   | Paranoia                          |
| 3    | 8   | Suicidal Thinking                 |
| 3    | 9   | Thoughts of Harming Others        |
| 3    | 99  | Other                             |
| 4    | 0   | Chest Pain/Pressure               |
| 4    | 1   | Irregular Heartbeat/Palpitations  |
| 4    | 2   | Swelling in Legs/Ankles           |
| 4    | 99  | Other                             |
| 5    | 0   | Dizziness                         |
| 5    | 1   | Extremity Numbness/Tingling       |
| 5    | 2   | Seizures                          |
| 5    | 3   | Headache/Migraine                 |
| 5    | 4   | Memory Loss                       |
| 5    | 5   | Gait Disturbance/Balance Problems |
| 5    | 99  | Other                             |
| 5    | 100 | Fainting                          |
| 6    | 0   | Easy Bleeding                     |
| 6    | 1   | Easy Bruising                     |
| 6    | 2   | Swollen Lymph Nodes               |
| 6    | 99  | Other                             |
| 7    | 0   | Double/Blurred Vision             |
| 7    | 2   | Redness/Discharge                 |
| 7    | 3   | Pain/Itching                      |
| 7    | 99  | Other                             |
| 8    | 0   | Hearing Loss                      |
| 8    | 1   | Sinus Pressure                    |
| 8    | 3   | Tooth Pain                        |
| 8    | 4   | Difficulty Swallowing             |
| 8    | 5   | Dry mouth/Sore Tongue             |
| 8    | 6   | Sore Throat/Hoarseness            |
| 8    | 7   | Nasal Drainage                    |
| 8    | 8   | Pain                              |
| 8    | 10  | Ringing                           |
| 8    | 11  | Allergies                         |
| 8    | 12  | Discharge                         |
| 8    | 13  | Decreased Smell                   |
| 8    | 99  | Other                             |
| 9    | 0   | Nasal Discharge                   |
| 9    | 1   | Sinus Pressure                    |
| 9    | 2   | Allergies                         |
| 9    | 3   | Decreased Smell                   |
| 9    | 99  | Other                             |
| 10   | 0   | Sore Throat/Hoarseness            |
| 10   | 1   | Cold Sores                        |
| 10   | 2   | Sore Tongue                       |
| 10   | 3   | Tooth Pain                        |
| 10   | 4   | Difficulty Swallowing             |
| 10   | 5   | Dry mouth/Sore Tongue             |
| 10   | 99  | Other                             |
| 11   | 0   | Cold/Heat Intolerance             |
| 11   | 2   | Excessive Thirst                  |
| 11   | 3   | Excessive Hunger                  |
| 11   | 4   | Generalized Weakness              |
| 11   | 99  | Other                             |
| 12   | 0   | Brittle Hair/Nails                |
| 12   | 1   | Hair Loss                         |
| 12   | 2   | Mole Changes                      |
| 12   | 3   | Rash                              |
| 12   | 4   | Skin Lesion                       |
| 12   | 5   | Laceration                        |
| 12   | 6   | Skin Discoloration                |
| 12   | 99  | Other                             |
| 13   | 0   | Abdominal Pain                    |
| 13   | 1   | Blood in Stool                    |
| 13   | 2   | Change in Stools                  |
| 13   | 3   | Constipation/Diarrhea             |
| 13   | 5   | Heartburn                         |
| 13   | 6   | Loss of Appetite                  |
| 13   | 7   | Nausea/Vomiting                   |
| 13   | 9   | Loss of Bowel Control             |
| 13   | 99  | Other                             |
| 14   | 0   | Back Pain                         |
| 14   | 1   | Joint Pain                        |
| 14   | 2   | Muscle Weakness/Cramps            |
| 14   | 3   | Neck Pain                         |
| 14   | 99  | Other                             |
| 15   | 0   | Contact Allergy                   |
| 15   | 1   | Food Allergies                    |
| 15   | 2   | Seasonal Allergies/Hay Fever      |
| 15   | 4   | Frequent Infections               |
| 15   | 99  | Other                             |
| 16   | 0   | Erectile Dysfunction              |
| 16   | 1   | Penile Discharge                  |
| 16   | 2   | Sexual Dysfunction                |
| 16   | 99  | Other                             |
| 17   | 0   | Abnormal Pap                      |
| 17   | 1   | Irregular Menses                  |
| 17   | 2   | Hot Flashes                       |
| 17   | 3   | Vaginal Discharge                 |
| 17   | 4   | Pain During Menstruation          |
| 17   | 5   | Pain During Intercourse           |
| 17   | 99  | Other                             |
| 18   | 0   | Abnormal Pap                      |
| 18   | 1   | Irregular Menses                  |
| 18   | 2   | Hot Flashes                       |
| 18   | 3   | Blood in Urine                    |
| 18   | 4   | Urinary Incontinence/Dribbling    |
| 18   | 5   | Slow Stream                       |
| 18   | 6   | Erectile Dysfunction              |
| 18   | 8   | Penile Discharge                  |
| 18   | 9   | Painful/Burning Urination         |
| 18   | 11  | Urinary Frequency                 |
| 18   | 12  | Vaginal Discharge                 |
| 18   | 13  | Pain During Menstruation          |
| 18   | 14  | Pain During Intercourse           |
| 18   | 99  | Other                             |
| 20   | 1   | ALTERED MENTAL SENSORIUM          |
| 20   | 2   | ABDOMINAL CRAMP/PAIN              |
| 20   | 3   | ANOREXIA                          |
| 20   | 4   | BLEEDING GUMS                     |
| 20   | 5   | BODY WEAKNESS                     |
| 20   | 6   | BLURRING OF VISION                |
| 20   | 7   | CONSTIPATION                      |
| 20   | 8   | CHEST PAIN/DISCOMFORT             |
| 20   | 9   | COUGH                             |
| 20   | 10  | DIARRHEA                          |
| 20   | 11  | DIZZINESS                         |
| 20   | 12  | DYSPHAGIA                         |
| 20   | 13  | DYSPNEA                           |
| 20   | 14  | DYSURIA                           |
| 20   | 15  | EPISTAXIS                         |
| 20   | 17  | FREQUENCY OF URINATION            |
| 20   | 18  | HEADACHE                          |
| 20   | 19  | HEMATEMESIS                       |
| 20   | 20  | HEMATURIA                         |
| 20   | 21  | HEMOPTYSIS                        |
| 20   | 22  | IRRITABILITY                      |
| 20   | 23  | JAUNDICE                          |
| 20   | 25  | LOWER EXTREMITY EDEMA             |
| 20   | 26  | MYALGIA                           |
| 20   | 27  | ORTHOPNEA                         |
| 20   | 28  | PALPITATIONS                      |
| 20   | 29  | SKIN RASHES                       |
| 20   | 30  | STOOL, BLOODY/BLACK TARRY/MUCOID  |
| 20   | 32  | SWEATING                          |
| 20   | 33  | SEIZURES                          |
| 20   | 34  | URGENCY                           |
| 20   | 35  | VOMITING/NAUSEA                   |
| 20   | 36  | WEIGHT LOSS                       |
| 20   | 37  | FEVER                             |
| 20   | 38  | PAIN                              |
| 20   | 99  | Others                            |

```sql
SELECT `review_of_system_types_id` as `type`, `type_key` as `key`, `label`
FROM `review_of_systems` WHERE (`language` = 'en') AND (`status` = '1')
ORDER BY review_of_system_types_id, type_key
```

### Review of Systems Types

| type | review_of_system_type        |
| ---- | ---------------------------- |
| 1    | Constitutional Symptoms      |
| 2    | Respiratory                  |
| 3    | Psychiatric                  |
| 4    | Cardiovascular               |
| 5    | Neurological                 |
| 6    | Hematologic/Lymphatic        |
| 7    | Eyes                         |
| 8    | Ears, Nose, Mouth and Throat |
| 11   | Endocrine                    |
| 12   | Integumentary/Breast         |
| 13   | Gastrointestinal             |
| 14   | Musculoskeletal              |
| 15   | Allergic/Immunologic         |
| 18   | Genitourinary                |
| 19   | Other                        |
| 20   | Sign and Symptoms            |

```sql
SELECT 
`type_key` as `type`, `review_of_system_type`
FROM `review_of_system_types` WHERE (`language` = 'en') AND (`active` = '1')
ORDER BY `type`
```

## Coding Systems

### For Naming Systems

| key                 | code                  | OID                      | uri                                                      | description                     |
| ------------------- | --------------------- | ------------------------ | -------------------------------------------------------- | ------------------------------- |
| `{{rxnorm}}`        | RxNorm                | 2.16.840.1.113883.6.     | http://www.nlm.nih.gov/research/umls/rxnorm              | The actual RXCUI for the RxNorm |
| `{{cpt}}`           | CPT                   | 2.16.840.1.113883.6.12   | http://www.ama-assn.org/go/cpt                           |                                 |
| `{{snomed_ct_int}}` | SNOMED_CT_INT         | 2.16.840.1.113883.6.96   | http://snomed.info/sct                                   |                                 |
| `{{icd10cm}}`       | Icd10CM               | 2.16.840.1.113883.6.90   | http://hl7.org/fhir/sid/icd-10-cm                        |                                 |
| `{{hcpcs}}`         | HCPCS                 | 2.16.840.1.113883.6.285  | https://www.cms.gov/Medicare/Coding/HCPCSReleaseCodeSets |                                 |
| `{{cvx}}`           | CVX                   | 2.16.840.1.113883.12.292 | http://hl7.org/fhir/sid/cvx                              |                                 |
| `{{loinc}}`         | LOINC                 | 2.16.840.1.113883.6.1    | http://loinc.org                                         |                                 |
| `{{}}`              | PH_ProviderCodes_NUCC | 2.16.840.1.113883.6.101  | http://nucc.org/provider-taxonomy                        |                                 |

### For Propietory Systems

| key           | description                    | code | OID | uri |
| ------------- | ------------------------------ | ---- | --- | --- |
| `{{rxqdrug}}` | **DoseSpot** Generic Drug Code | -    | -   | -   |

### For Vendor Product

| key | source                            |
| --- | --------------------------------- |
| 1   | AllScripts Pro                    |
| 2   | DoseSpot Staging                  |
| 3   | AllScripts TouchWorks             |
| 4   | Change Healthcare Labs            |
| 5   | Point Click Care                  |
| 6   | Athena Health                     |
| 7   | eClinical Works CCDA              |
| 8   | drchrono CCDA                     |
| 9   | athenahealth CCDA                 |
| 10  | Enable Healthcare Inc. (EHI) CCDA |
| 11  | CCDA import                       |
| 12  | Greenway CCDA                     |
| 13  | Practice Fusion CCDA              |
| 14  | MWell                             |
| 15  | DHIT CCDA                         |
| 16  | Adventus                          |
| 17  | Medilink                          |
| 18  | Medicard                          |
| 19  | DHIT SSO                          |
| 20  | MMMC                              |

```sql
SELECT `id` as `key`, `source`
-- , `description`, `ehr_vendor`
FROM `records_alt_source`;
```

## For Media Files

### Image Category

| key | message |
| --- | ------- |
| 0   | Photo   |
| 1   | Xray    |
| 2   | MRI     |
| 3   | CT Scan |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 18
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '18') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Tracing Category

| key | message    |
| --- | ---------- |
| 0   | ECGs       |
| 1   | Spirometry |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 22
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '22') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Audio Category

| key | message |
| --- | ------- |
| 0   | Heart   |
| 1   | Lung    |
| 2   | Bowel   |
| 3   | Other   |
| 4   | Speech  |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 19
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '19') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### Document Category

| key | message                  |
| --- | ------------------------ |
| 0   | Labs                     |
| 1   | Imaging                  |
| 2   | OT/PT                    |
| 3   | Speech                   |
| 4   | Behavioral/Psych         |
| 5   | Medical                  |
| 6   | Other Documents          |
| 7   | Authorizations           |
| 8   | Other Consultations      |
| 9   | Legal                    |
| 10  | Medical Records          |
| 11  | Information              |
| 12  | Manuals                  |
| 13  | Audiology                |
| 14  | Ophthalmology            |
| 15  | Other Labs               |
| 16  | Surgical                 |
| 17  | CCDA                     |
| 18  | Signed Encounter Summary |
| 19  | --                       |
| 20  | Dermatology              |
| 21  | Pain Management          |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 17
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '17') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

## For Billing

### Transaction Type

| key | message                 |
| --- | ----------------------- |
| 0   | none                    |
| 1   | check-in                |
| 2   | check-out               |
| 3   | on account              |
| 4   | by patient              |
| 5   | dpc enroll              |
| 6   | dpc subscription        |
| 7   | copay                   |
| 8   | refund                  |
| 9   | billing adjustment      |
| 10  | PRMS billing adjustment |

```sql
-- Table: transactions_types
SELECT `transaction_type` as `key`, `description` as `message`
FROM `transactions_types`
ORDER BY `key`
```

### Billable Type

| key | message      |
| --- | ------------ |
| 0   | insurance    |
| 1   | patient-pay  |
| 3   | prv          |
| 4   | dpc          |
| 5   | patient-resp |
| 6   | refund       |
| 7   | prompt-pay   |

```sql
-- Table: billable_types
SELECT `billable_type` as `key`, `description` as `message`
FROM `billable_types`
ORDER BY `key`
```

### Billing Status

| key | message              |
| --- | -------------------- |
| 0   | Not Billed           |
| 1   | Billed               |
| 2   | Paid in Full         |
| 3   | Questions            |
| 4   | Billing Code Changed |
| 8   | Not Charged          |
| 9   | Ignore               |
| 11  | Unbilled             |
| 12  | Rebilled             |
| 13  | Billed to DPC        |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 93
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '93') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```

### No Show Types

| key | message                                                   |
| --- | --------------------------------------------------------- |
| 0   | Patient not in Consult Room                               |
| 1   | Audio Problems (Video is OK)                              |
| 2   | Video Problems (Audio is OK)                              |
| 3   | No Audio and Video                                        |
| 4   | Connectivity issues (Doctor has poor internet connection) |
| 5   | Re-decked to attending physician                          |
| 6   | For rescheduling                                          |
| 7   | Triaged to Specialist                                     |
| 8   | Triaged to ER/F2F                                         |
| 9   | Doctor did not hear/see the notification                  |
| 10  | Doctor not on duty                                        |
| 11  | Others, specify:                                          |

```sql
-- Table: ref_dictionaries
-- dictionary_types_id: 94
SELECT `type_key`  as `key`, `label` as `message`
FROM `ref_dictionaries`
WHERE (`dictionary_types_id` = '94') AND (`language` = 'en')
AND `label` <> ''
ORDER by `key`
```
