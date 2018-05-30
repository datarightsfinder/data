# Open Data Rights database

## Contents

* [Things to know](#things-to-know)
* [Template](#template)
* [Schema](#schema)
* [Standard formats](#standard-formats)
* [Types of personal data](#type-of-personal-data)
* [Clarity ratings](#Clarity-ratings)

## Things to know

* Files should be named in the format `[company name].json`. Each filename should be unique.

* Everything is optional apart from `organisationInfo`. This is so we can relate an organisations information with information from [OpenCorporates](https://opencorporates.com).

* International companies have complicated structures. As a rule, we use the OpenCorporates information for the parent company.

* `null` is an acceptable value for any field if information for it can't be found in a privacy policy.

* Alternatively, omitting a field means information hasn't been actively looked for.

## Template

For an empty template with spaces for all possible values, see [template.json](#).

## Schema

### `organisationInfo` (mandatory)

Basic information about the organisation so it can be linked with information from [OpenCorporates](https://opencorporates.com).

| Name | Type | Description |
| ---- | ---- | ----------- |
| country | string | The [ISO 3166-2 code](https://en.wikipedia.org/wiki/ISO_3166-2) for where an organisation is registered. For example `us_de` or `gb`
| number | string | The unique identifier used by the country to identify the organisation |
| urls | array[string] | An array of URLs associated with this organisation |

### `dataProtectionOfficer`

Information about the [Data Protection Officer](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/accountability-and-governance/data-protection-officers/) at an organisation.

| Name | Type | Description |
| ---- | ---- | ----------- |
| name | string | Name of the Data Protection Officer |
| role | string | Role of the Data Protection Officer if they also take another role |
| contactInfo | [contactInfo](#contactinfo) | Information about how to contact the Data Protection Officer |

### `internationalTransfer`
Compliance information about organisations that transfer data outside the EEA.

| Name | Type | Description |
| ---- | ---- | ----------- |
| privacyShieldUrl | string | Link to an organisations entry on the [US-EU Privacy Shield Framework](https://www.privacyshield.gov) register |
| dataProcessingAddendum | [dataProcessingAddendum](#dataprocessingaddendum) | See [dataProcessingAddendum](#dataprocessingaddendum) for more details |

### `privacyNotice`

A link to an organisations main privacy policy.

| Name | Type | Description |
| ---- | ---- | ----------- |
| url | string | Link to an organisations privacy notice page |

### `dataProtectionRegister`

Information about a company from a national data regulators register of data processors, like the [Information Commissioner's Office register of fee payers](https://ico.org.uk/about-the-ico/what-we-do/register-of-fee-payers/).

| Name | Type | Description |
| ---- | ---- | ----------- |
| identifier | string | An identifier used in a national regulators database of data processors |
| url | string | A link to an organisations page on a national regulators database of data processors |

### `thirdParties`

Other organisations that process personal data on behalf of an organisation.

| Name | Type | Description |
| ---- | ---- | ----------- |
| list | array[string] | An array of strings containing the names of organisations used as third parties |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

### `retentionRules`

How long an organisation keeps types of personal data.

| Name | Type | Description |
| ---- | ---- | ----------- |
| rules | array[[retentionRule](#retentionrule)] | An array of [retention rule objects](#retentionrule) |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

### `dataTypesCollected`

What types of personal information a company collects.

| Name | Type | Description |
| ---- | ---- | ----------- |
| list | array[string] | An array of strings that represent the data an organisation collects. See [data types](#data-types) for possible values. |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

### `automatedDecisionMaking`

Information about this organisations use of automated decision making.

| Name | Type | Description |
| ---- | ---- | ----------- |
| usesAutomatedDecisionMaking | boolean | `true` or `false` depending on whether a company uses automated decision making |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

## `lawfulBases`

Information about the [six reasons](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/lawful-basis-for-processing/) organisations use to justify the processing of personal data.

| Name | Type |
| ---- | ---- |
| consent | [lawfulBasis](#lawfulbasis) |
| contract | [lawfulBasis](#lawfulbasis) |
| legalObligation | [lawfulBasis](#lawfulbasis) |
| vitalInterests | [lawfulBasis](#lawfulbasis) |
| publicTask | [lawfulBasis](#lawfulbasis) |
| legitimateInterests |[lawfulBasis](#lawfulbasis) |

### `rights`

Information for individuals around exercising their [new personal data rights](https://ico.org.uk/for-organisations/guide-to-the-general-data-protection-regulation-gdpr/individual-rights/).

| Name | Type |
| ---- | ---- |
| access | [rightInfo](#rightinfo) |
| rectification | [rightInfo](#rightinfo) |
| erasure | [rightInfo](#rightinfo) |
| restrictProcessing | [rightInfo](#rightinfo) |
| dataPortability | [rightInfo](#rightinfo) |
| object | [rightInfo](#rightinfo) |
| automatedDecisionMaking | [rightInfo](#rightinfo) |

### `complaintInformation`

Information about making a complaint to a regulator in a privacy notice.

| Name | Type | Description |
| ---- | ---- | ----------- |
| hasInformation | boolean | `true` or `false`, depending on whether a privacy notice has clear information about how to make a complaint |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

### `securityStandards`

Information about how a company protects personal data.

| Name | Type | Description |
| ---- | ---- | ----------- |
| url | string | Link to a page about how a company secures information |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

## Standard formats

### `contactInfo`

Must contain one or more of four possible values.

| Name | Type | Description |
| ---- | ---- | ----------- |
| url | string | A full URL like `https://example.com`|
| postalAddress | string | A postal address like `123 Test Avenue, London, WC2R 1LA, United Kingdom` |
| emailAddress | string | An email address like `example@example.com` |
| telephoneNumber | string | A telephone number with international dialing code like `+4402071234567`|

### `dataProcessingAddendum`

A Data Processing Addendum enables a non-EEA company to process data on behalf of an EEA company while meeting obligations under GDPR. Some countries are considered by the European Commission to have an [adequate level of protection](https://ec.europa.eu/info/law/law-topic/data-protection/data-transfers-outside-eu/adequacy-protection-personal-data-non-eu-countries_en), so don't require any other arrangements.

For other countries, the European Commission have written [Model Clauses](https://ec.europa.eu/info/law/law-topic/data-protection/data-transfers-outside-eu/model-contracts-transfer-personal-data-third-countries_en) that organisations can adopt in their Terms of Service to become GDPR compliant. These are usually entered into by signing a document or changing a setting. Sometimes model clauses are already in a Terms of Service.

| Name | Type | Description |
| ---- | ---- | ----------- |
| type | string | `form`: a digital or printed form has to be returned<br>`setting`: a data processing addendum can be entered into through changing a setting<br>`assumed`: the main Terms of Service includes a EU compatible data processing agreement |
| url | string | The URL of where to access the form or setting to enter into a data processing addendum |
| notes | string | Free text to provide additional information |

### `retentionRule`

Used to describe how long a type of personal data is kept.

| Name | Type | Description |
| ---- | ---- | ----------- |
| type | string | A single data type from our [list of data types](#data-types) or `general` |
| duration | string | How long a data type is retained for, for example, `30 days`, `6 months` or `2 years`

### `rightInfo`

Contains contact information on how to exercise each individual personal data right.

| Name | Type | Description |
| ---- | ---- | ----------- |
| contactInfo | [contactInfo](#contactinfo) | A [contactInfo](#contactinfo) object containing one or more ways to exercise this right |
| notes | string | Free text for further explanation |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

### `lawfulBasis`

| Name | Type | Description |
| ---- | ---- | ----------- |
| notes | string | Free text explaning why this lawful basis was chosen and what data it applies to |
| clarity | integer | See [clarity ratings](#clarity-ratings) |

## Types of personal data

TODO

## Clarity ratings

We use a number between 0 and 3 to label how easy a bit of information is to understand.

* `0` Non-existant
* `1` Difficult to understand
* `2` Moderately difficult to understand
* `3` Easy to understand
