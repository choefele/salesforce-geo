# Salesforce Location Experiments

## Storing Coordinates in Contact

* [Find coordinate](https://www.gps-coordinates.net)
* Update coordinate on `Contact`:
```
List<Contact> contacts=[select Id, Name from Contact where LastName='Test' limit 1];

if (!contacts.isEmpty()) {
   	Contact contact=contacts[0];
   	contact.MailingLatitude = 52.520904;
    contact.MailingLongitude = 13.351403;
   	update contact;
    
   	System.debug('Updated contact: ' + contact);
} else {
	System.debug('Contact not found');
}
```
* Query `Contact`s ([reference](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_geolocate.htm)):
```
SELECT Id, Name, MailingLatitude, MailingLongitude
FROM Contact
ORDER BY DISTANCE(MailingAddress, GEOLOCATION(37.775,-122.418), 'km')
LIMIT 10
```