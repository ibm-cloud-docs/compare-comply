---

copyright:
  years: 2015, 2021
lastupdated: "2021-01-25"

subcollection: compare-comply

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:preview: .preview}
{:beta: .beta}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Information security
{: #information-security}

{{site.data.keyword.cncfull}} is discontinued. Existing instances are supported until 30 November 2021, but as of 1 December 2020, you can't create instances. Any instance that exists on 30 November 2021 will be deleted. Consider migrating to {{site.data.keyword.discoveryshort}} Premium on {{site.data.keyword.cloud_notm}} for your {{site.data.keyword.cncshort}} use cases. For more information, see the [announcement](/status?query=Compare+and+Comply&selected=announcement){: external}.
{: deprecated}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation. Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients’ business and any actions the clients may need to take to comply with such laws and regulations.
{: important}

The products, services, and other capabilities described herein are not suitable for all client situations and may have restricted availability. IBM does not provide legal, accounting or auditing advice or represent or warrant that its services or products will ensure that clients are in compliance with any law or regulation.

If you need to request GDPR support for {{site.data.keyword.cloud}} {{site.data.keyword.watson}} resources that are created

- In the European Union (EU), see [Requesting support for IBM Cloud Watson resources created in the European Union](/docs/watson?topic=watson-gdpr-sar#request-EU).
- Outside of the EU, see [Requesting support for resources outside the European Union](/docs/watson?topic=watson-gdpr-sar#request-non-EU).

## European Union General Data Protection Regulation (GDPR)
{: #gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here](https://www.ibm.com/data-responsibility/gdpr){: external}.

## Labeling and deleting data in the {{site.data.keyword.cncshort}} service
{: #delete-data}

The {{site.data.keyword.cncshort}} service enables you to delete all data that is associated with feedback and batch-processing requests. To delete data, you must do the following:

1.  Use the `X-Watson-Metadata` header to associate a customer ID with data that is passed by a request to the service; see [Specifying a customer ID](/docs/compare-comply?topic=compare-comply-information-security#specify-customer-id).
1.  Use the `DELETE /v1/user_data` method to delete all data that is associated with a specified customer ID; see [Deleting data](/docs/compare-comply?topic=compare-comply-information-security#delete-cnc).

By default, no customer ID is associated with data.

Experimental and beta features are not intended for use with a production environment and therefore are not guaranteed to function as expected when labeling and deleting data. Experimental and beta features should not be used when implementing a solution that requires the labeling and deletion of data.
{: note}

### Specifying a customer ID
{: #specify-customer-id}

To associate a customer ID with data, include the `X-Watson-Metadata` header with the request that passes the information. You pass the string `customer_id={id}` as the argument of the header. The following example associates the customer ID `my_ID` with the data passed with a `POST /v1/feedback` request:

```bash
curl -X POST -u "apikey:{apikey}" \
--header "X-Watson-Metadata: customer_id=my_ID" \
--header "Content-Type: application/json" \
--header "Accept: application/pdf" \
--data "{feedback_data}" \
"{url}/v1/feedback?version=2018-10-15" \
```
{: pre}

A customer ID can include any characters except for the `;` (semicolon) and `=` (equals sign). Specify a random or generic string for the customer ID; do not specify a personally identifiable string, such as an email address or Twitter ID. You can specify different customer IDs with different requests. A customer ID that you specify is associated with the instance of the service whose credentials are used with the request; only credentials for that instance of the service can delete data associated with the ID.

Use the `X-Watson-Metadata` header with the following methods:

- `POST /v1/batches`
- `POST /v1/feedback`
- `GET /v1/feedback`
- `GET /v1/feedback/{feedback_id}`

The customer ID is associated with data that is sent with the request.

### Deleting data
{: #delete-cnc}

To delete all data that is associated with a customer ID, use the `DELETE /v1/user_data` method. You pass the string `customer_id={id}` as a query parameter with the request. The following example deletes all data for the customer ID `my_ID`:

```bash
curl -X DELETE -u "apikey:{apikey}" "{url}/v1/user_data?customer_id=my_ID"
```
{: pre}

The `DELETE /v1/user_data` method deletes all data that is associated with the specified customer ID, regardless of the method by which the information was added. The method has no effect if no data is associated with the customer ID. You must issue the request with credentials for the same instance of the service that was used to associate the customer ID with the data.

## Health Insurance Portability and Accountability Act (HIPAA)
{: #cnc-hipaa}

US Health Insurance Portability and Accountability Act (HIPAA) support is available for Premium plans in the Washington, DC location created on or after 1 April 2019. See [Enabling EU and HIPAA supported settings](/docs/account?topic=account-eu-hipaa-supported){: external} for more information.
