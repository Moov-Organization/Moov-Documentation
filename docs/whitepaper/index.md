
# Moov Ride Hailing Whitepaper

> This documentation is not finalized and may undergo significant rework.

## Introduction: An Overview of Transportation

Transportation is essential to modern living. From the earliest innovations - shoes, horses, wagons, etc. - to the relatively recent innovations of railways, aeroplanes, and automobiles, humanity has always sought to improve the ease, speed, cost, and efficiency of transportation. People have a wide variety of contemporary transportation options, but they each have their own specific advantages and drawbacks.

Personal transportation (a user-owned automotive) is perhaps the best method of meeting on-demand transportation today. Personal vehicles are limited in range only by the ability of the owner to refuel, and the existence of land to drive on. However, owning a car can be expensive - there's the base vehicle cost, insurance, fuel, regulation checks, and maintenance and registration (and these are just the personal costs). More so, personally owning a vehicle is an incredibly inefficient use of space and time. On average, personal vehicles are [parked 95% of the time](https://www.reinventingparking.org/2013/02/cars-are-parked-95-of-time-lets-check.html). Not only does this mean that car owners generally have a return of only 5% of the value of their vehicle, but there are draws on land allocation to accommodate these parked cars. For precious real estate in city centers, this can be a contentious issue. Lastly, personal vehicles tend to depreciate in value quite rapidly.

Directly contrasting the concept of personally-owned vehicles is the notion of [Transportation as a Service (TaaS)](https://en.wikipedia.org/wiki/Transportation_as_a_Service) in which transportation is provided by an external entity. Transportation services can come in several forms.

Public transportation is one expression of TaaS which greatly improves on the space and time efficiency of the vehicle - buses, trams, and railways tend to serve routes all day, unless in need of maintenance. In addition, most municipalities offer ride plans that reduce the overall cost of transportation when taken frequently; compared to personal vehicles, public transportation is quite inexpensive, yielding [high savings](http://www.apta.com/mediacenter/pressreleases/2017/Pages/June-Transit-Savings.aspx) in cities with strong services. Naturally, public transportation has disadvantages. For one, bus and railway routes are fixed along centralized paths without any way to connect to fringe locations. Thise looking to access the periphery of a town would need to walk from the closest stop on the route. In addition, public transportation often follows strict timing, meaning the transprotation-on-demand of a personal vehicle is lost with this service.

Taxi services are another alternative. Taxis retain transportation-on-demand, but are often relatively expensive solutions that are designed for single, infrequent trips. In addition, taxi services often have [local monopolies due to regulation](https://www.cagw.org/thewastewatcher/and-medallion-goes-%E2%80%A6-taxicab-monopoly) which drives up the difficulty of breaking into the market as a new driver or service provider. Therefore drivers cannot set their own rates, and are at the whim of the singular stewarding company.

The most recent addition to available transportation methods are the "ride hailing" services, most notably Lyft and Uber. These services perform very similarly to taxi services, however they also provide a set of other integrated services including ride hailing and tracking, and electronic payment via phone apps (we will refer to this set of services simply as the ride hailing stack). The primary advantage of these providers is ease of interfacing - all relevant information is bundled into once place. However, like the taxi services, drivers employed by these centralized services cannot set their own rates, and are reliant on the ride hailing stack offered by the steward companies. This means that drivers and riders alike are still potentially subject to oligopolistic conditions in the long term using this transportation method. In addition, these technologies do not exist in a vacuum; with the advent and rising popularity of autonomous vehicles, it is likely that ride hailing companies will eventually move to automated fleets, further building conditions making market entry difficult.

We believe that a more ideal transportation solution can be found, which combines the best features of all of the noted observed methods.

## Proposal of Improvements

We propose a decentralized public-stake ride hailing system with user-owned manned fleets.

To understand the functionality of this proposed system, we must break down what today's ride hailing services provide. All ride hailing providers offer a core seven services:
- Matchmaking for connecting riders to drivers
- Recommended price estimation
- Price negotiation
- Payment processing and escrow
- Dispute-handling for riders or drivers that break contract
- Driver and vehicle registration and verification

At minimum, the proposed system must be able to provide all of these services with the ease of access that current ride hailing systems have.

Current ride hailing providers combine all of these services into a single closed-source vertical market, which has the side-effect of increasing barriers to entry to market, and therefore encouraging oligopolies. However, it is not necessary that a single entity provides all of the constituent services. In an alternate scenario, a horizontal market could be established by opening up the interfaces between these services so that new parties could provide each service individually. Engendering a horizontal market also innately encourages competition; since the services are no longer bundled into a single vertical market, services can be developed individually, and therefore with less upfront cost.

Under this proposed system, if an individual is dissatisfied with their existing service provider, they can switch providers or start their own service provider entity. In today's market, setting up a new service provider would be prohibitively difficult - it would be necessary to provide the entire stack of services with similar performance to existing services.

Flattening the market may also reduce the cost of the final service, since competition typically drives down prices.

Decentralizing the system ensures that there is no single point of failure which could cause the system to become unavailable simultaneously.

The system envisioned should also be adaptable to new technologies; specifically, it should be able to naturally transition to a fleet of autonomous vehicles when adoption of the technology is more widespread. However, these vehicles should still be either user-owned or publicly-owned (municipal) in order to maintain public stake in the system.

Lastly, the system should not force any significant additional complexity on the end users - riders and drivers.

With these qualities in mind, we can specify a protocol which would meet these system demands.

## Moov Ride Hailing System Specification (v0.1)

### Architecture

> @todo write me based on the "v1.0" section below

----
> @todo continue editing below this line:
> - design decisions could use trimming
> - reduce size of images, use XML-generated images from something like draw.io
> - revise v1.0 for service-oriented descriptions and make sure new system jives
> - consider removing sections below v1.0 section; extraneous or should be moved to business/values doc

> - cut down on content in v0.1-0.4 and move info to rebuttals section(s)
> - provide user-friendly blog as intro to tech, hand-holding
> - v1.0 section should list:
>   - definitions of service provider entities
>   - operation chain of the protocol at large
>   - definitions of message formats for all external interfaces (to user/driver and blockchain)
>   - optionally, message formats for internal systems as well
>   - analysis of performance
> - provide counterarg + rebuttal after v1.0 proposal section
----
> @todo use the below but do not feel obliged to keep it
----
## Design Decisions Background

### Simple Decentralized Ride hailing (v0.1)

![v0.1](img/v0_1.jpg)

This is the simplest implementation of a decentralized ride hailing marketplace as shown in the demo. A smart contract is hosted on the blockchain, a rider pings the smart contract with a ride request containing the pickup and dropoff location attached with the money(in protocol tokens) they are willing to pay. On the other end of smart contract, drivers are listening to the queue of ride requests and the first one to accept a ride request receives it. After the driver picks up and drops off the rider at specified location, the rider will command the smart contract to release the money to the driver.

This prototype demonstrates how a purely decentralized ride hailing service can be built without the need for any middlemen. However, there are some drawbacks.

User Perspective:
- Riders do not know the correct price for a particular ride, thus they are expected to take random guesses.
- Drivers cannot be pragmatically expected to sieve through the massive number of ride requests and find the one that gives them the best bang for their buck.
- There is no inherent mechanism to handle disputes between the driver and rider.

Technical Perspective:
- All the interactions happen on chain, which can be very slow and inefficient.

### Uber Plugged In to the Blockchain (v0.2)

![v0.2](img/v0_2.jpg)

In this model a new entity has been added, the matchmaker. Riders fill a ride request with the pick up and drop off locations, authorized matchmaker, matchmaker fee(in protocol tokens) and maximum money they are willing to pay(in protocol tokens), then sign it and send it to the matchmaker. When the matchmaker receives a ride request, it will match the request with the best driver based on parameters like location, rating, price etc. The matchmaker will then forward the request to a driver, if the request meets the driver’s requirement, he will sign it and send it back matchmaker, who will then forward entire request to the blockchain for processing. The blockchain will verify the signatures then notify the driver, after the driver picks up and drops off the rider at specified location, the rider will command the smart contract to distribute the money to the parties as agreed. However, if there is a dispute, the blockchain will kick the transaction back to the matchmaker and ask it to resolve the dispute.
Although this is a step up, it is basically Uber using the blockchain for payment processing instead of Visa or Amex. As this model scales it will likely produce monopolies due to the network effect or the winner-take-all effect. Since the probability of finding the best match is directly dependent on the amount of traffic flowing through the matchmaker, it is likely for a few matchmakers to become too big. Consequently the barrier to entry for a new matchmaker will be high resulting in reduced competition thus hampering the process of capitalism.

![v0.2 scaling](img/v0_2_scale.jpg)

### Dismantled Uber (v0.3)

![v0.3](img/v0_3.jpg)

In this model a new entity has been added, the ride manager(guy with megaphone) who is incharge of broadcasting ride requests received from riders. On the other hand, the matchmaker is only incharge of going through the ride requests broadcasted by different managers and finding the best match for its drivers. Adding the ride manager decouples the broadcasting and ride matching layers thus taking care of the network effect. As this model scales it is significantly less likely to produce oligopolies.

![v0.3 scaling](img/v0_3_scale.jpg)

### With Integration of State Authority (v0.4)

![v0.4](img/v0_4.jpg)

In this model the government or its transportation regulating authority is also included, where it directly or indirectly(through authorized 3rd parties) verifies drivers and their vehicles for meeting the minimum safety requirements. It has to then add the the addresses of the verified drivers to a license registry hosted on the blockchain. Whenever new ride requests are sent to the chain for processing, the processing smart contract will verify that the driver address is present in the license registry. Integrating the government into the chain also allows the government to easily collect taxes to fund their invaluable services like road maintenance and emergency services.

## Ride Hailing Protocol Version 1
> @todo populate with new info
> @todo this protocol needs a proper name

The detailed steps of the ride hailing process:

![v1.0](img/v0_3_detail.jpg)

1. Rider will use the generic Moov phone app with which he can connect to any of the ride managers, while some ride managers may have their custom apps. The rider will connect with a certain ride manager and tell it where he wants to go. The ride manager will analyze current market data and respond with an estimated price and a maximum price. Through the app the rider will sign a ride request containing pickup location, drop off location, maximum price(in protocol tokens), address of the matchmaker and the matchmaker fee
2. The matchmaker will receive the request and conduct a subsecond period auction of the ride request. If anybody agrees to accept the ride request at the advertised price the manager will award it to them otherwise the manager will incrementally advertise the ride request for higher prices till the maximum price indicated by the user.
3. On the other end there will be a host of matchmakers each connected to a group of drivers with authorization from the drivers to pick up a ride request on their behalf. The matchmakers will do a quick math to see if a ride request will be a proper match for any one of its drivers in terms of time and money, if yes then the matchmaker will sign an accept request message containing the transaction hash of the ride request, the driver address and the matchmaker address and then send the accept request to the manager.
4. The manager will pick up the first accept request, close the auction, sign and send both requests to the smart contract hosted on the blockchain for verification.
5. If both requests are valid, that is the rider has enough money and the matchmaker has been authorized by the driver, the smart contract will approve the request and move money from the rider’s account to itself. The blockchain will also send a notification to the manager and the matchmaker.
6. The matchmaker will forward the notification to the driver.
7. Once the driver gets the notification, he will pick up and drop off the rider as per agreement and then both parties will notify the smart contract.
8. If both parties indicate to the smart contract that weren’t any issues, the smart contract will then distribute the money as agreed earlier.
9. (Conditional)However, if one of the parties raises an issue the smart contract will dispatch a dispute request to the manager and authorize the manager to distribute the money as the manager sees fit. The manager will examine the evidences, award the money to the party it judges to be correct and take a part of the disputed amount as fees for the service of handling the dispute.

This model is more immune to oligopolization because of the proper separation of services. It is extremely easy for the rider to move from one ride manager to another. The barrier to entry for a new manager or a new matchmaker is extremely low. It is also easy for the drivers to move between matchmakers. This ease of movement and low barrier to entry will increase competition, which will reduce cost and improve quality of service overtime.

### FAQ

1. Is this a decentralized or a trustless service?

Although this model is significantly more decentralized than uber or lyft it is not a fully decentralized or a trustless service. In this model riders trust that the ride managers will be honest about the ride estimation and micro auction process. However the revenue model for the ride manager is based on loyalty, so it is of utmost importance for them that their riders do not lose trust, otherwise they could easily leave them. Similarly, drivers trust matchmakers to find the best match for them, again the revenue model for the matchmaker is also based on loyalty. So it is of utmost importance for them that their drivers do not lose trust, otherwise they could easily leave them for another provider.

2. Why do ride managers conduct micro auctions?

Negotiating prices is usually a process that takes a lot of back and forth. Imagine multiple ride managers and matchmakers negotiating at the same time, it could become a very noisy process. But by making the ride managers conduct micro auctions, the number of interactions between the manager and matchmaker is drastically minimized.

3. How are the fees for manager and matchmaker allocated?

Usually a manager will specify a flat fee to host a ride request and specify a percentage cut of the disputed amount if it has to resolve disputes. On the other end, matchmakers will specify a percentage cut to drivers for finding them the best match.

4. How are drivers and vehicles enforced to meet minimum safety requirements?

This will be addressed in the next version.

### Scalability

Even though this a significantly better model than the current one for ride hailing services, it cannot be realized till there are scalable implementations of the blockchain. On average Uber dispatches about 150 rides every second whereas today’s top smart contract service provider, the ethereum virtual machine, can only process about 15 transactions per second. Not to forget, there are thousands of other smart contracts competing for transaction space within the ethereum virtual machine. As the passenger economy enlarges over the coming years, there may be several thousand ride requests per second. As of now there is not a decentralized blockchain out there that can meet such a demand. So that is the risk we face and we are betting that within a few years a scalable blockchain that can meet our transactional requirements will be available. If that is not the case, we are not opposed to developing a chain that is tailored to our needs.

### Market Analysis

When riders make a ride request, they will specify the ride amount in dollars but since the blockchain does not have an inherent understanding of dollars, the dollar amount will be converted to a protocol token, called Moov tokens. With about 10% of the American population as active users, uber’s total revenue for the year 2017 was 37 billion dollars. If the protocol mentioned above was used instead, the transactional load per year on the protocol tokens would have been 37 billion dollars. America is touted to become a passenger economy over the next few decades. If that is the case, significant portion of the remaining 90% of the population will be using mobility as a service instead of owning cars. According to a study published by intel, ride hailing economy is posited to be worth 400 billion dollars per year in 15 years and 3 trillion dollars per year in 30 years. So if Moov protocol becomes the standard protocol to make rides in the future, the transactional load on the protocol tokens maybe billions or trillions of dollars per year.

### Our Plan

We plan to issue a limited number protocol tokens and sell them as utility tokens. We will use the money to develop the Moov smart contract which will enable the Moov ride hailing protocol showcased above. Not only that we will also develop a suite of open source software that will incentivize the adoption of the Moov protocol. This suite of software will include:
1. An open source version of the ride manager.
2. An open source version of the phone app riders will use to connect with the ride manager.
3. An open source version of a data aggregator which will collect current ride request data and builds a real time heat map.
4. An open source version of a machine learning algorithm that mines through the aggregated ride request data and predicts future ride requests heat map.
5. An open source version of a AI credit rater which goes through the trove of available information and gives each rider and driver a rating.
6. An open source version of the matchmaker which will use 3, 4 & 5 in conjunction with its internal AI software to find the best matches for its drivers.
7. An open source version of the app drivers will use to connect with the matchmaker.

All these open sourced tools will significantly lower the entry for anyone to become one of the service providers in our ecosystem, thus increasing the adoption rate of our protocol.

### The "Kicker"

That is not all the technology we plan to develop that will increase the adoption of the Moov protocol, we also plan to develop open source self driving technology. This technology will be open under a limited license where the source code will be open and individuals can use it for personal use for free. However if they want to use the technology for commercial purposes(make money using it) they will have apply for a commercial license. The commercial license will be granted on an agreement along the lines of:
“Licensed parties may use the software to offer taxi services commercially and if they use the Moov network they can keep all the money they make to themselves. However, if they chose to use another ride hailing network or use it for commercial purposes other than taxi services then they will have to donate a portion of the money to an open source project of our choosing.”

We plan to develop a logic board that will enable any vehicle to become a self driving vehicle granted the sensors and actuators of the vehicle meet specified requirements and interface with the board using specified protocols. We will also get this board safety certified by the top safety certifying companies in the world. We will then partner with car manufacturers from around the world to install this board in their vehicles. There would be incentive for them to partner with us because we would giving them the ability to add safety certified self driving capabilities to their cars for almost free. They would only have to pay for the cost of manufacturing the board. This reduction in cost will directly be translated to the end consumers (especially the drivers who depend on driving as a livelihood) to easily afford a self driving car.

This board and it’s commercial license will be critical in the increasing the adoption of the protocol and funding the development of more open source projects.

Again we plan to fund the development of the protocol and the suite of technology aimed at increasing its adoption through the sale of the limited number of protocol tokens. In the future, these protocol tokens will be used as utility tokens by riders to move from one part of the world to another.

> @todo determine what other sections need to be here
