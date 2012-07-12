Digital Government Strategy
===========================

This repository serves as the canonical machine-readable schema for describing action items within the president's digital strategy, and for reporting on its progress. Citizen developers are encouraged to use this information to build applications and tools. As agencies place their `digitalstrategy.{format}` reporting file at the root level of their agency's primary domain, developers could use the agency list included to retrieve an individual agency's progress, or to aggregate agencies' progress as a whole.

API
---

The files contained in this repository are available as a psuedo-service using the following syntax:

`https://raw.github.com/GSA/digital-strategy/{api_version}/{file}.{format}`

Examples:

[`https://raw.github.com/GSA/digital-strategy/1/agencies.xml`](https://raw.github.com/GSA/digital-strategy/1/agencies.xml)

[`https://raw.github.com/GSA/digital-strategy/1/items.json`](https://raw.github.com/GSA/digital-strategy/1/items.json)


Files
-----

* `agencies.json` and `agencies.xml` - machine-readable listing of common federal agencies, their primary domain, and abbreviation (e.g., FBI)
* `items.json` and `items.xml` - machine-readable representation of the action items from the digital strategy

Reporting
---------
To comply with the presidential memorandum's reporting requirements, each reporting agency should generate `digitalstrategy.xml` and `digitalstrategy.json` files which meet the schema described herein and should place such files at the top level of their primary domain e.g., `agency.gov/digitalstrategy.json` and `agency.gov/digitalstrategy.xml`. A human-readable version of the same information (not restricted to any specific format or schema) should also be placed at `agency.gov/digitalstrategy` or `agency.gov/digitalstrategy.html` for agenies with a content management system or similar publishing platform.

To create a report file, agencies could use the tool(s) provided by GSA, or could generate the files using their own means, so long as such generated files conform to the established schema. Agencies creating tools or applications to this end are encouraged to share their tools publicly and with other agencies.

Report files as substantially similar to the base schema file contained within this repository, however, when reporting, agencies should propegate their answers into the `value` field of each action item. Multiple values are to be represented as an array of values in JSON, and as a child `value` node in XML.

Data Types and Standards
------------------------

In the interest of compatability and interoperability, unless otherwise noted, no field or value should contain any tags or markup.

Agency List
-----------

The agency list contains a timestamp of when the file was last updated as well as a listing of common federal agencies. Each agency has three fields:

* **name** - The Human-readable name of the agency (e.g., Federal Communications Commission)
* **id** - The agencies abbreviation or id (e.g., fcc)
* **url** - the agency's primary domain (e.g., www.fcc.gov)

In JSON this is represented as:

```json

{
   "generated":"2012-07-12 10:46:19",
   "agencies":[
      {
         "name":"Administrative Conference of the United States (ACUS)",
         "id":"acus",
         "url":"www.acus.gov"
      },
      {
         "name":"Advisory Council on Historic Preservation (ACHP)",
         "id":"achp",
         "url":"www.achp.gov"
      },
      ...
   ]
}
```

In XML this is represented as:

```xml
<?xml version="1.0"?>
<agencies>
  <generated>2012-07-12 10:46:19</generated>
  <agencies>
    <agency id="acus">
      <name>Administrative Conference of the United States (ACUS)</name>
      <url>www.acus.gov</url>
    </agency>
    <agency id="achp">
      <name>Advisory Council on Historic Preservation (ACHP)</name>
      <url>www.achp.gov</url>
    </agency>
    ...
  </agencies>
</agencies>
```

Items
-----

The items act as a machine-readable representation of the agency-specific action items outlined in the digital strategy, as well as a base schema for reporting on its progress. At the root level, the schema contains a timestamp indicating when it was last updated, as well as a list of all action items.

Each action item can have the following properties:

* **id** - a unique identifier for that action item, e.g., 2.1
* **parent** - where applicable, the parent action item, (e.g., 2.2.1's parent would be 2.1). Useful for grouping and formatting
* **text** - the human-readable text of the action item
* **due** - when the action item is due (relative to the release of the digital strategy)
* **due_date** - date calculated as the abosolute due date for the action item
* **fields** - a list of all fields associated with that action item
* **multiple** - whether multiple responses are allowed per action item (e.g., listing multiple systems with each of the action-item's field being answered once per system)

The field object is made up the following:

* **type** - the HTML input type that best represents the field (e.g., select, text, textarea)
* **name** - HTML friendly name for the field
* **label** - Human readable label for the field
* **option** - where applicable, an array of label, value pairs describing the potential options (e.g. for a drop down)
* **value** - when used as an agency progress report, the agency-reported answer to the field, or if multiple answers, an array of agency-reported answers. Multiple values will be represented as an array in JSON, as nested `value` nodes in XML.

In JSON this would be represented as:

```json

{
   "generated":"2012-07-12 11:00:27",
   "items":[
      {
         "id":"2.1",
         "parent":null,
         "text":"Engage with customers to identify at least two existing major customer-facing services that contain high-value data or content as first-move candidates to make compliant with new open data, content, and web API policy.",
         "due":"90 Days",
         "due_date":"2012\/08\/20",
         "fields":[
            {
               "type":"select",
               "name":"2-1-status",
               "label":"Overall Status",
               "options":[
                  {
                     "label":"Not Started",
                     "value":"not-started"
                  },
                  {
                     "label":"In Progress",
                     "value":"in-progress"
                  },
                  {
                     "label":"Completed",
                     "value":"completed"
                  }
               ],
               "value":null
            }
         ],
         "multiple":false
      },
      ...
   ],
}
```

In XML this would be represented as:

```xml

<?xml version="1.0"?>
<items>
  <generated>2012-07-12 11:00:27</generated>
  <items>
    <item id="2.1">
      <parent/>
      <text>Engage with customers to identify at least two existing major customer-facing services that contain high-value data or content as first-move candidates to make compliant with new open data, content, and web API policy.</text>
      <due>90 Days</due>
      <due_date>2012/08/20</due_date>
      <fields>
        <field>
          <type>select</type>
          <name>2-1-status</name>
          <label>Overall Status</label>
          <options>
            <option>
              <label>Not Started</label>
              <value>not-started</value>
            </option>
            <option>
              <label>In Progress</label>
              <value>in-progress</value>
            </option>
            <option>
              <label>Completed</label>
              <value>completed</value>
            </option>
          </options>
          <value/>
        </field>
      </fields>
      <multiple/>
    </item>
    ...
  </items>
</items>
```

Additional Resources
--------------------

Please feel free to use the project wiki to share any additional resources related to the project.