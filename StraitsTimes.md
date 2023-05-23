# The Straits Times (new version) / XML file parser - Detail design specification

<!-- TOC -->

- [The Straits Times (new version) / XML file parser - Detail design specification](#the-straits-times-new-version--xml-file-parser---detail-design-specification)
    - [Overview](#overview)
    - [Referring material](#referring-material)
    - [Parser app file name](#parser-app-file-name)
    - [Data source](#data-source)
        - [File naming](#file-naming)
        - [Timezone](#timezone)
        - [Delivery Timing from Providers](#delivery-timing-from-providers)
        - [Sample data](#sample-data)
        - [Data layout](#data-layout)
    - [Database access and data mapping logic](#database-access-and-data-mapping-logic)
    - [Considerations](#considerations)

<!-- /TOC -->

## Overview
- This material describes the detail design of module which is scraping the data provided by **The Straits Times** publisher.

## Referring material
- [Endless FTP fetcher - Function design specification](../../../fd/fd_fetcher/fd_endless_ftp-fetcher.md)  
- [XML file parser - Function design specification](../../../fd/fd_parser/fd_xml-file-parser.md)  
  - [XML file parser - Detail design specification](./index.md)  

## Parser app file name
- straits_times_xml_file_parser.py

## Data source
- The following content describes the original data source provided by **Sphdigital server**.  

### File naming

- sti_search_YYYYMMDD.xml

### Timezone
- The timezone of the date that XML file has is UTC+08:00.

### Delivery Timing from Providers
- Delivery date : Everyday (between 9:30 and 10:30 JST).  
    - The scuedule is changed by atrticle type.  

### Sample data
- This xml layout is written in XML format (not RSS format).  

**Object:**  

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<content>
<article>
    <pub>BTO</pub>
    <artid>278326</artid>
    <vcmid/>
    <launchdate>2020-01-14 21:25:00.0</launchdate>
    <expirydate>2020-01-15 03:59:00.0</expirydate>
    <paid_mode>0</paid_mode>
    <print>0</print>
    <copyright>SPH</copyright>
    <category1><![CDATA[ Companies & Markets ]]></category1>
    <category2><![CDATA[ ]]></category2>
    <link><![CDATA[ https://www.businesstimes.com.sg/companies-markets/miyoshi-sinks-into-red-with-q1-net-loss-of-s314000 ]]></link>
    <kick><![CDATA[  ]]></kick>
    <headline1><![CDATA[ Miyoshi sinks into red with Q1 net loss of S$314,000 ]]></headline1>
    <headline2><![CDATA[  ]]></headline2>
    <abstract><![CDATA[ MANUFACTURER Miyoshi on Tuesday posted a net loss of S$314,000 for its first quarter ended Nov 30, compared to a net profit of S$4.3 million a year ago. ]]></abstract>
    <content><![CDATA[ <p>MANUFACTURER Miyoshi on Tuesday posted a net loss of S$314,000 for its first quarter ended Nov 30, compared to a net profit of S$4.3 million a year ago.</p> <p>Revenue dipped 3.5 per cent to S$14 million from S$14.5 million a year ago, mainly due to lower sales orders from the data storage and automotive segments in China and the Philippines. This was partially offset by higher revenue from the consumer electronics segment and higher rental income from the renewed tenancy agreement for its investment properties in the Philippines.</p> <p>Loss per share was 0.01 cent, a reversal from earnings per share of 0.71 cent a year ago.</p> <p>The bottom line fell because of the absence of a one-off gain on disposal of its Singapore industrial property at 5 Second Chin Bee Road, as well as a share of loss from associate of about S$367,000, which reflects the share of results of loss-making Chinese electric vehicle company Core Power, which Miyoshi has invested in.</p> <p>Miyoshi had previously disclosed that its independent auditors, BDO LLP, had included a qualified opinion on the group's FY19 financial statements mainly in connection with its investment in Core Power, a foreign associate.</p> <p>"The management of the company is in active discussions with Core Power to resolve the financial-reporting matters," it said.</p> <p>The company added that the global economic environment continues to present challenges as the group faces business headwinds.</p> <p>"The trade tensions between the US and China are expected to continue to exert a negative impact on our business performance in our associated company in China. Our outlook for the next 12 months remains cautious."</p> ]]></content>
    <author><![CDATA[ Lee Meixian ]]></author>
    <author_email><![CDATA[ leemx@sph.com.sg ]]></author_email>
    <author_twitter><![CDATA[ @LeeMeixianBT ]]></author_twitter>
    <title><![CDATA[ Miyoshi sinks into red with Q1 net loss of S$314,000 ]]></title>
    <pullquote><![CDATA[  ]]></pullquote>
    <object><![CDATA[  ]]></object>
    <thumbnail><![CDATA[  ]]></thumbnail>
    <caption><![CDATA[  ]]></caption>
    <video><![CDATA[ ]]></video>
  </article>
</content>    
```

### Data layout

- The following json layout is made from xml file. The following content describes the data mapping compared with xml layout and json layout.The original xml data should be changed the following json layout according to the mapping rule.  

**Object:**  

```json
{
    "Uuid" : "a8098c1a-f86e-11da-bd1a-00112444be1e",
    "UniqueRecord" : "TheStraitsTimes#278326",
    "ProviderCode" : "TheStraitsTimes",
    "ProviderArticleId" : 278326,
    "ProviderSource" : "https://www.straitstimes.com/global",
    "ProviderImage" : "",
    "ProviderTitle" : "",
    "ProviderDescription" : "sti_search_20180421.xml",
    "FirstDisplayTime" : "1524268800",
    "LastBuildDate" : "1524268800",
    "ArticleTitle" : "![CDATA[ Miyoshi sinks into red with Q1 net loss of S$314,000 ]]",
    "ArticleDescription" : "![CDATA[ MANUFACTURER Miyoshi on Tuesday posted a net loss of S$314,000 for its first quarter ended Nov 30, compared to a net profit of S$4.3 million a year ago. ]]",
    "ArticleContent" : "![CDATA[ <p>MANUFACTURER Miyoshi on Tuesday posted a net loss of S$314,000 for its first quarter ended Nov 30, compared to a net profit of S$4.3 million a year ago.</p> <p>Revenue dipped 3.5 per cent to S$14 million from S$14.5 million a year ago, mainly due to lower sales orders from the data storage and automotive segments in China and the Philippines. This was partially offset by higher revenue from the consumer electronics segment and higher rental income from the renewed tenancy agreement for its investment properties in the Philippines.</p> <p>Loss per share was 0.01 cent, a reversal from earnings per share of 0.71 cent a year ago.</p> <p>The bottom line fell because of the absence of a one-off gain on disposal of its Singapore industrial property at 5 Second Chin Bee Road, as well as a share of loss from associate of about S$367,000, which reflects the share of results of loss-making Chinese electric vehicle company Core Power, which Miyoshi has invested in.</p> <p>Miyoshi had previously disclosed that its independent auditors, BDO LLP, had included a qualified opinion on the group's FY19 financial statements mainly in connection with its investment in Core Power, a foreign associate.</p>]",
    "CanonicalUrl" : "https://www.businesstimes.com.sg/companies-markets/miyoshi-sinks-into-red-with-q1-net-loss-of-s314000",
    "Category" : "![CDATA[ Companies & Markets ]]",
    "CategoryId" : "![CDATA[ Companies & Markets ]]",
    "PubDate" : "1524268800",
    "ProvidedDataTimezone" : "+08:00",
    "Visible" : true,
    "EnableDisplayBody" : false,
    "Payload" : {
        "Subtitle" : "![CDATA[  ]]",
        "Subcategory" : "",
        "CopyrightLine" : "SPH",
        "Kicker" : "![CDATA[ ]]",
        "Byline" : "![CDATA[ Lee Meixian ]]"
    },
    "CreatedAt": "96892058814",
    "ModifiedAt": "1527848435",
    "ExecutedTimezone": "+09:00",
    "S3FilePath" : "TheStraitsTimes/Done/20200605/strait_business_times_new_ftp_server/breaking_news/ST/{origin xml file name}.xml",
    "DefaultLanguage" : "en"
}
```

**Mapping rule:**  

| source (xml)            | distination (json)    | description                                                                                                                                    | relation key |
|:------------------------|:----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|:-------------|
|                         | Uuid                  | Generate the random value with UUID (uuid.uuid4())                                                                                             | no           |
|                         | ProviderCode          | Fix value: TheStraitsTimes                                                                                                                     | **yes**      |
| body.article.id         | ProviderArticleId     | It just only be moved xml value to json value.                                                                                                 | **yes**      |
|                         | ProviderSource        | Fixed value : https://www.straitstimes.com/global                                                                                              | no           |
|                         | ProviderImage         | Set empty.                                                                                                                                     | no           |
| head                    | ProviderTitle         | Only moving xml value to json value.                                                                                                           | no           |
|                         | ProviderDescription   | Pick up XML file name and set it into JSON field.                                                                                              | no           |
|                         | FirstDisplayTime      | Date : Pick up XML file name, convert to **UTC epoch sec** format                                                                              | no           |
|                         | LastBuildDate         | Date : Pick up XML file name, convert to **UTC epoch sec** format                                                                              | no           |
| body.article.headline1  | ArticleTitle          | Only moving xml value to json value. (See &#8727;1)                                                                                            | no           |
| body.article.abstract   | ArticleDescription    | Only moving xml value to json value. (See &#8727;1)                                                                                            | no           |
| body.article.content    | ArticleContent        | Only moving xml value to json value. (See &#8727;1)                                                                                            | no           |
| body.article.link       | CanonicalUrl          | There is no data to set here.                                                                                                                  | no           |
| body.article.category1  | Category              | Only moving xml value to json value.                                                                                                           | no           |
| body.article.category1  | CategoryId            | Only moving xml value to json value.                                                                                                           | **yes**      |
| body.article.launchdate | PubDate               | Moving xml value to json value, convert to **UTC epoch sec** format                                                                            | no           |
|                         | ProvidedDataTimezone  | Fixed value : +08:00 (This value is local timezone of the provider)                                                                            | no           |
|                         | Visible               | Refer the data in Settings.json, ftp_fecher_settings.json, sftp_fetcher_settings.json                                                          | no           |
|                         | Visible               | Refer the data in Settings.json, ftp_fecher_settings.json, sftp_fetcher_settings.json                                                          | no           |
| body.article.headline2  | Payload.Subtitle      | Only moving xml value to json value.                                                                                                           | no           |
| body.article.category2  | Payload.Subcategory   | Only moving xml value to json value.                                                                                                           | no           |
| body.article.copyright  | Payload.CopyrightLine | It just only be moved xml value to json value.                                                                                                 | no           |
| body.article.kick       | Payload.Kicker        | Only moving xml value to json value.                                                                                                           | no           |
| body.article.author     | Payload.Byline        | Only moving xml value to json value.                                                                                                           | no           |
|                         | CreatedAt             | Current executed DateTime for insert, format **UTC epoch sec**                                                                                 | no           |
|                         | ModifiedAt            | Current executed DateTime for insert/update, format **UTC epoch sec**                                                                          | no           |
|                         | ExecutedTimezone      | Fixed value : +09:00 (The timezone that Parser app launches in Japan)                                                                          | no           |
|                         | UniqueRecord          | Set the value of `ProviderCode`#`ProviderArticleID` to json value                                                                              | **yes**      |
|                         | S3FilePath            | File path on S3:<br />**{ProviderCode}**/Done/**{YYYYMMDD}**/strait_business_times_new_ftp_server/**{category}**/ST/{origin xml file name}.xml | no           |
|                         | DefaultLanguage       | "en"                                                                                                                                           | no           |

- &#8727;1：This data should be escaped.  
- &#8727;2：Payload has only an object.  
- &#8727;3：1 xml file contain array `body.article[]` that each `article` of it need convert to one json file.

## Database access and data mapping logic
1. Generate json data based on the XML file. 
1. It should be decided the CRUD rule depending on returning data
   1. **Insert:** 
      1. Not exist data
		 - It should be checked that `ProviderCode, ProviderArticleId` not exist in DynamonDB.
   1. **Update:**
	  1. Already exist data
		 - It should be checked that `ProviderCode, ProviderArticleId` exist in DynamonDB.
   1. **Delete:** 
	  1. Not provided deletion as this function.  

## Considerations
- It doesn't need to handle `life_search_YYYYMMDD.[xX][mM][lL]`, this file is not put into S3.  
    - `[xX][mM][lL]` means `xml file extention`.  
- The empty file is put on Dahlia server at Monday and Tuesday. It doesn't need to intent to the spec that is put the empty file into Dahlia server. Nikkei developers can handle the empty files which are put on Dahlia. 
    - Wed : The data of `Digital Life`.  
    - Thu : The data of `Mind Your Body`.  
    - Fri : The data of `Urban`.  
