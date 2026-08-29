# Resilient Session Layer for IRCTC Booking
A hackathon prototype that solves the most severe IRCTC user pain point: 
unexpected forced logout during ticket booking.

## Problem
A national survey of 90,000+ passengers identified “forced logout” as the 
most disruptive IRCTC dark pattern. Users lose their booking progress 
mid-journey, especially during Tatkal hours.

## Solution
We introduce a Resilient Session Layer that:
- Refreshes session TTL on every user action
- Adds a “Reserved / PendingPayment” state
- Holds seats for 5 minutes (grace timer)
- Prevents forced logout under heavy load
- Uses synthetic data and mocks payment
- Preserves the complete citizen journey

## Architecture
- **Sticky Load Balancer**: keeps user on same server
- **Session Manager**: sliding TTL refresh
- **Redis Cluster**: session store + atomic counters
- **Lua Scripts**: atomic TTL extension
- **Reservation State**: temporary seat hold
- **Observability**: Prometheus + Grafana

## Citizen Journey
Search → Select → Details → Review → Reserved → Mock Payment → Confirmation

## Compliance
- No access to real IRCTC systems
- No real payment or OTP flows
- All data is synthetic
- No government logos or implied affiliation

## Demo
- `before.html`: forced logout simulation
- `after.html`: stable session + reservation state
- `index.html`: final improved version (hosted)

## Branding
This prototype includes the Sadhyaware logo and link to ai.sadhyaware.com, 
which is permitted as personal branding and does not imply government affiliation.

## Future Work
- Distributed session replication
- Adaptive TTL based on user behavior
- Fairness algorithms for seat reservation
- Exponential backoff for retry flows
- Multi-region Redis clustering

