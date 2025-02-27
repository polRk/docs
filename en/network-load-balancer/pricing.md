---
editable: false
---
# Pricing for {{ network-load-balancer-name }}



{% include [currency-choice](../_includes/pricing/currency-choice.md) %}

When using {{ network-load-balancer-full-name }}, you are charged for the incoming traffic processed by a network load balancer and for the number of network load balancers.

Outgoing traffic is charged the same as for other {{ yandex-cloud }} services, such as [Compute Cloud](../compute/pricing.md#prices-traffic). Charges for outgoing traffic include the traffic that is generated when targets respond to health checks.

## Pricing {#prices}

### Using an internal load balancer {#internal-load-balancer}

The [internal load balancer](concepts/internal-load-balancer.md) functionality is at the [Preview](../overview/concepts/launch-stages.md) stage and can be used free of charge.

### Incoming traffic {#prices-traffic}

You are charged for incoming traffic to the IP address and port specified as the network load balancer's listener. Any other traffic directed to the load balancer is not accepted and is not charged.




{% include [usd.md](../_pricing/network-load-balancer/usd-ingress.md) %}


### Network load balancers {#network-load-balancers}

You are charged for network load balancers if they have a listener and a non-empty target group attached.

If a network load balancer has no target groups attached but has a listener, then the public IP address of the listener is charged as an [inactive public IP address](../vpc/pricing.md#prices-public-ip).




{% include [usd.md](../_pricing/network-load-balancer/usd-balancer.md) %}


