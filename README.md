### DEX401 - Anypoiont Development Fundamentals Classroom Reference - 260223 - MST

Vincent Lowe

vlowe@salesforce.com

Cloudshare Login Link: https://use.cloudshare.com/Class/yk7ui

Passphrase: Scarlet the Trustworthy Wombat

-------------------------------------------------------------------------------------------------------------------

Trailhead Academy: https://trailheadacademy.salesforce.com/my-learning

Attendance Code: 3C5O0M

Salesforce Mimeo: https://salesforce.mimeo.digital/MuleSoft

eBook Redemption Key: USMQ9SOFQGT8

-------------------------------------------------------------------------------------------------------------------

Survey Link: https://www.research.net/r/trailheadacademy

Survey ID: TASM-041561

-------------------------------------------------------------------------------------------------------------------
Zoom Link: <<Zoom Link>>

Meeting ID: <<Meeting ID>>

Class Setup (pre-class): https://trailhead.salesforce.com/help?article=Computer-Setup-Guide-for-MuleSoft-Expert-Led-Classes#DEX401

Advanced REST Client:
https://install.advancedrestclient.com/

Postman:
https://www.postman.com/downloads/

Help:
https://help.mulesoft.com/

Docs:
https://docs.mulesoft.com

Log Analyzer Tool:
https://help.mulesoft.com/s/article/Support-Log-file-analyzer-tool

Status:
https://status.mulesoft.com 
   
------------------------------------------------------------------------------

Java VM: https://docs.mulesoft.com/general/java-support

MuleSoft Pricing & Support: https://www.mulesoft.com/anypoint-pricing

Einstein for Anypoint Code Builder: https://videos.mulesoft.com/watch/Z3Xzk8RFds5erbzLASev1W

Log Analyzer: https://help.salesforce.com/s/articleView?language=en_US&id=Support-Log-file-analyzer-tool&type=1

------------------------------------------------------------------------------
Anypoint Platform: 
https://anypoint.mulesoft.com

|Track Title|Artist|Notes|
|-----------|------|-----|
|Smooth Criminal|Luca Stricagnoli|Find the YouTube video on this - you will be amazed|
|My Rifle, My Pony And Me|Dean Martin and Ricky Nelson|from the movie Rio Bravo|
|This Old Town|Nanci Griffith||
|The Hitter|Mark Erelli|Mark wrote this for his son|
|Man of Constant Sorrow|Geoff Castellucci|All voices on the track are Geoff|
|The City of New Orleans|Arlo Guthrie||
|Can't Find My Way Home|Bonnie Raitt|Stevie Winwood cover|
|Just Breathe|Willie Nelson with Lukas Nelson|Eddie Vedder cover|
|Tupelo Honey|Reina del Cid|she records as Elle Cordova now|
|Can't Let Go|Lucinda Williams||
|Dos Oruguitas|Stephen Joseph|Instrumental cover of song from Encanto|
|Vincent Harp Solo|Vincent|It's the only song he knows on harmonica|
|Analog Hero|Mark Erelli||
|Hello Goodbye|The Beatles||
|Good Day for a Good Day|Michael Franti and Spearhead||
|How Can You Mend a Broken Heart|Al Green|Bee Gees cover|
|Sixteen Tons|Geoff Castellucci||
|Foggy Mountain Breakdown|Earl Scruggs||


	<flow name="getDeltaFlights" doc:id="576a29f5-1bdd-4ed8-89b1-0af7a53e5d2e" >
		<http:listener doc:name="GET /delta" doc:id="5e04bc01-1e55-451f-a230-845f754528c5" config-ref="mua-flights-api-httpListenerConfig" path="/delta"/>
		<flow-ref doc:name="setDestination" doc:id="58f50b4b-9434-4861-84ec-7e436fc8a699" name="setDestination"/>
		<ee:transform doc:name="map input data" doc:id="89f4f97e-bfa0-40f7-91ed-c1a9f3982bae" >
			<ee:message >
				<ee:set-payload ><![CDATA[%dw 2.0
output application/xml
ns ns0 http://soap.training.mulesoft.com/
---
{
	ns0#findFlight: {
		destination: vars.destination
	}
}]]></ee:set-payload>
			</ee:message>
		</ee:transform>
		<wsc:consume doc:name="Delta Flights" doc:id="80984984-18d6-455d-806f-61417a01f372" config-ref="Delta_Consumer_Config" operation="findFlight"/>
		<ee:transform doc:name="to canon" doc:id="6f784d2e-a162-40c8-b10c-76d24181d4bf" >
			<ee:message >
				<ee:set-payload ><![CDATA[%dw 2.0
output application/json
ns ns0 http://soap.training.mulesoft.com/
---
payload.body.ns0#findFlightResponse.*return map ( return , indexOfReturn ) -> {
	airline: return.airlineName default "",
	flightCode: return.code default "",
	fromAirportCode: return.origin default "",
	toAirportCode: return.destination default "",
	departureDate: return.departureDate default "",
	emptySeats: return.emptySeats default 0,
	price: return.price default 0,
	planeType: return.planeType default ""
}]]></ee:set-payload>
			</ee:message>
		</ee:transform>
	</flow>



	



