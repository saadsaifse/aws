## Route 53

* Highly available, scalabale, fully managed, authoritative DNS (customer has full control in updating the DNS records)
* A domain registrar
* Only AWS service that has 100% SLA
* 53 is a reference to original DNS port
* Routes traffic for a domain based on DNS records such as
  * A -> eIPV4
  * AAAA -> IPV6
  * CNAME -> Another hostname
    * Can't create cname for top node of a DNS namespace (Zone Apex) e.g., can't create for example.com, but can create for www.example.com
  * NS -> Name servers for the hosted zone that are corresponding to the DNS queries
* Routing policy: how route53 respond to queries
* TTL: time to live for a record in DNS resolvers

### Hosted Zones

* A container for records that define how the traffic is routed for a domain or subdomain
  * Public hosted zones: public domains
  * Private hosted zones: route traffic within a VPC
* $0.5 per month per hosted zone

