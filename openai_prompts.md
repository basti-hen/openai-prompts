# GPT-3 examples (using mostly text-davinci-003)

## Information extraction from claim phone conversations

* Engine: text-davinci-003 (also works in text-davinci-002, but might require more instructions to get a correct JSON back)
* Temperature: 0.7

```
You must extract the following information from the phone conversation below:

1. Call reason (key: reason)
2. Cause of the incident (key: cause)
3. Names of all drivers as an array (key: driver_names)
4. Insurance number (key: insurance_number)
5. Accident location (key: location)
6. Car damages as an array (key: damages)
7. A short, yet detailed summary (key: summary)

Make sure fields 1 to 6 are answered very short, e.g. for location just say the location name
Please answer in JSON machine-readable format, using the keys from above.

Phone conversation:
Hi I just had a car accident and wanted to report it. OK, I hope you're alright, what happened? I was driving on the I-18 and I hit another car. Are you OK? Yeah, I'm just a little shaken up. That's understandable. Can you give me your full name? Sure, it's Sarah standl. Do you know what caused the accident? I think I might have hit a pothole. OK, where did the accident take place? On the I-18 freeway. Was anyone else injured? I don't think so. But I'm not sure. OK, well we'll need to do an investigation. Can you give me the other drivers information? Sure, his name is John Radley. And your insurance number. OK. Give me a minute. OK, it's 546452. OK, what type of damages has the car? Headlights are broken and the airbags went off. Are you going to be able to drive it? I don't know. I'm going to have to have it towed. Well, we'll need to get it inspected. I'll go ahead and start the claim and we'll get everything sorted out. Thank you.

JSON:
```
## News article processing

* Engine: text-davinci-003 (won't work well with 002)
* Temperature: 0.7

(News article courtesy of WDR - [link](https://www1.wdr.de/nachrichten/themen/coronavirus/corona-isolationspflicht-nrw-102.html))

```
Extract information from the news article below. In detail, please perform:

1. one sentence summary in German
2. All names
3. All German States

Return the results in a JSON document with the keys summary, names, and states.

News article:
Die Isolationspflicht für Corona-Infizierte steht in NRW auf der Kippe. Die Landesregierung plant eine Entscheidung. Außerdem sollen die Corona-Regeln am Arbeitsplatz im Februar enden. In NRW könnte die Isolationspflicht für Corona-Infizierte bald enden. Gesundheitsminister Karl-Josef Laumann (CDU) kündigte am Mittwoch eine Entscheidung der Landesregierung in dieser Frage an. Ein konkretes Datum nannte er jedoch nicht. "Ich kann nur sagen, dass ich davon ausgehe, dass bis auf Sachsen, Berlin und Brandenburg am 1. Februar alle Länder aus der Isolationspflicht raus sind", sagte er über die Situation in anderen Bundesländern. Die Landesregierung prüfe, ob NRW noch dabei bleibe oder nicht. Bayern, Schleswig-Holstein, Rheinland-Pfalz und Hessen seien bereits vor Weihnachten aus der Isolationspflicht rausgegangen und die Corona-Zahlen hätten sich dort nicht anders entwickelt als in den Bundesländern mit einer Isolationspflicht. "Dann wären im Grunde genommen alle landesrechtlichen Regelungen weitestgehend - wenn man das dann so machen würde - am 1. Februar raus", sagte Laumann.

Results:
```

## Information retrieval and data formatting

* Engine: text-davinci-002 or better
* Temperature: 0.7

Classify companies into verticals:
```
Classify Microsoft, UBS, SAP, FedEx and Zurich Insurance into their verticals.
```

Change formatting:
```
Classify Microsoft, UBS, SAP, FedEx and Zurich Insurance into their verticals. Write the answer as COMPANY#INDUSTRY. Do not write it as a ordered list, but write a new line for each.
```

Add revenue:
```
Classify Microsoft, UBS, SAP, FedEx and Zurich Insurance into their verticals. Also add the yearly revenue for each company. Write the answer as COMPANY#INDUSTRY#REVENUE. Do not write it as a ordered list, but write a new line for each.
```

Format revenue:
```
Classify Microsoft, UBS, SAP, FedEx and Zurich Insurance into their verticals. Also add the yearly revenue for each company. Write the answer as COMPANY#INDUSTRY#REVENUE. Write revenue as $x.xxbn. Do not write it as a ordered list, but write a new line for each.
```

## Dealing with missing data / avoiding hallucination

* Engine: text-davinci-002 or text-davinci-003 (text-davinci-003 is less prone to suffer from hallucination)
* Temperature: 0.7

Bad:
```
If a vehicle will be used at any time, proof of automobile liability insurance is required with the following limits of coverage: $500,000 limit minimum combined single limit.

Are the children insured?
```

Better:
```
If a vehicle will be used at any time, proof of automobile liability insurance is required with the following limits of coverage: $500,000 limit minimum combined single limit.

Are the children insured? If the answer is not in the text, write "Answer not found".
```

## Getting more precise answers by asking for explanations

* Engine: text-davinci-002 or text-davinci-003
* Temperature: 0.7

Might return a highly incorrect result (not always though):
```
What is the annual energy demand in kWh for a single-family household with four people. Assume they are home 330 days per year.
```

Typically returns an accurate result:
```
What is the annual energy demand in kWh for a single-family household with four people. Assume they are home 330 days per year.
Please think step by step and explain the calculation step by step.
```

## Information extraction from NDAs

* Engine: text-davinci-003
* Temperature: 0.7

```
From the following NDA, please extract the following information:

- When the contract was signed
- Who signed the contract
- Address of the person signing the contract
- Fine for breaching the contract

Answer in JSON. Use the keys signing_date, name, address, and fine_amount. Format the signing_date as MM/DD/YYYY.

NDA:
On the date of August 17th, 2019, as an employee of Contoso Restaurant, I, Mateo Gomez, residing in 1234 Hollywood Boulevard Los Angeles CA, with social security number: 123-45-6789, hereby declare to fully support and promote the top priorities delegated to me at Contoso Restaurant, and vow to never disclose any information including but not limited to trade secrets, finances, delivery schedules, and recipes.
If I, Mateo Gomez, accidentally or with intent breach the conditions set forth in this contract, understand fully that I shall receive a written termination to the following email address mateo@contosorestaurant.com as well as a fine of up to $10,000.

Extracted information in JSON:
```

## Letter writing in German

* Engine: text-davinci-003 (won't work well with text-davinci-002)
* Temperature: 0.7

```
Wartungsfenster für den 14. Februar von 14 bis 15 Uhr geplant, da Leitungsarbeiten, erwarten sie Ausfallszeiten.

Schreibe einen formalen Brief an die Kunden in Deutsch
- Biete Hilfe unter info@operations.de an
- Bitte um Verzeihung
- Benutze 00:00 als Zeitformat

Brief:
```

## Extract content from company documents

* Engine: text-davinci-003 
* Temperature: 0.7

```
Dear Shareholders, 
2021 was a year in which we once again accelerated the implementation of our strategy and translated it into fascinating products and financial success. At the same time, we were able to further increase our financial resilience. This has been key to steering the company through industry-wide challenges – from the ongoing pandemic to global semiconductor supply short- ages. We also successfully achieved an historical milestone: the spin-off and hive-down of the Daimler commercial vehicle business. As a well-focused company, we in the Mercedes-Benz Group AG can make even better use of the opportunities that lie ahead. We are a vehicle manu- facturer – and we are proud to be. This is now also reflected in the name of the company. 
Last year, a total of 2.3 million customers opted for a passenger car or a van with a star. Our revenue amounted to €168.0 billion. EBIT increased by 340% to €29.1 billion. Our net liquidity in the industrial business amounted to €21.0 billion. The bottom line was a net profit of €23.4 bil- lion. The Board of Management and the Supervisory Board will propose a dividend of €5.00 per share to the Shareholders' Meeting. 
For this performance, gratitude is due to all colleagues. The past year was characterised by a challenging environment and high volatility. We successfully countered this – with strict discipline and great flexibility. This tremendous commitment and a strong team spirit are also crucial to continue the success story. 
As we look ahead, we need to limit the impact of supply shortages, counter rising commodity prices, and continue to work on our cost efficiency. In addition, we pursue clear strategic priori- ties: we want to scale e-mobility, accelerate software development, and further strengthen Mercedes-Benz as a leading luxury brand. 
We continue to focus on the electrification of our products. This year, we are presenting two all-electric off-road vehicles. It is important to ensure a smooth launch. At the same time, we need to scale our electric vehicles. This year, we are going to offer an electric alternative in all segments. We plan to increase our share of electrified vehicles to account for up to 50% for overall sales by 2025. And by the end of this decade, we are going to be ready to switch com- pletely to electric, where market conditions permit this. Our Maybach, AMG, and G-Class brands are also becoming all-electric. We are significantly expanding our global activities in battery cells and battery systems in order to make these plans successful. With the presentation of the Vision EQXX, we reinforced our claim to be the innovative leader in electromobility. The concept car gives a glimpse of what may be possible in the future in terms of efficiency and electric range. 
Our second technological spearhead is acceleration in the area of software. In particular, this also implies the expansion of our competence in this area. We are creating up to 3,000
new jobs worldwide – a significant proportion of these at our centre of excellence for software in Sindelfingen. There we want to push the development of our own operating system in a bundled effort. And in automated driving, we are launching the next stage: Mercedes-Benz is the first manufacturer in the world to receive internationally valid system approval to introduce highly automated driving functions at level 3 to series production cars. That is what we will do in Germany this year. 
The technological change is the basis for the successful transformation of Mercedes-Benz into an automotive brand in the luxury segment. The initial position is excellent: innovative technology, emotional design, and attention to detail – this is what Mercedes-Benz has represented for
over 100 years. With the new structure, we have bundled our strength. Our ultimate goal: to build the most desirable cars and vans in the world. This transformation did not start today and it will not be done tomorrow – it is the responsibility of our generation. And that is where unique opportunities lie. In this context, the Mercedes star is a promise for the future: we want to change what exists in order to improve it. This is the spirit that our founding fathers gave us. We will carry on their legacy. I look forward to you joining us on this journey. 
Yours, 
Ola Källenius 
 

Please tell me
1) summarize the year 2021 of Mercedes-Benz
2) What risks did impact the business?
3) What is the outlook?
4) Who wrote the text?
5) What is on the roadmap?
6) what is the sentiment of this text?
```

## Extract technical information

* Engine: text-davinci-003 
* Temperature: 0.7

```
CLA 250 e Coupé CLA 250 e Shooting Brake
Displacement cc 1,332 1,332
Rated output, petrol engine kW/hp 120/163 120/163
at rpm 5,500 5,500
Rated torque, petrol engine Nm 270 270
Rated power, electric motor kW/hp 80/109 80/109
Rated torque, electric motor Nm 300 300
System output kW/hp 160/218 160/218
System torque Nm 450 450
Rated battery capacity kWh 15.6 15.6
Combined fuel consumption, weighted (WLTP provisional) l/100 km 1.1-0.8 1.1-0.8
Combined CO2 emissions, weighted (WLTP provisional) g/km 24-18 26-19
Combined power consumption, weighted (WLTP provisional) kWh/100 km 16.9-14.9 17.2-15.1
Electric range (EAER) (WLTP provisional) km 71-82 68-80
Acceleration 0-100 km/h s 7.6 7.7
Top speed km/h 229 226
###

Please answer the following questions based on the given input:

What are the CO2 emissions of the CLA250 Shooting Brake? 
And the CLA250 coupé? 
What is the top speed of the Shooting Brake?
```

## Generate apps

This is similar to ChatGPT, which can generate code snippets/full simple apps.

* Engine: text-davinci-003
* Temperature: 0.7

```
Write a Flask app that shows a simple hello world website with a html template.
```

Then after the example has been generated, add the following prompt:

```
Add an API that returns the weather data for a location that the user can enter in a textbox on the hello.html site.
```

# Codex examples (using mostly code-davinci-002)

```python
# Table customers, columns = [CustomerId, FirstName, LastName, Company, Address, City, State, Country, PostalCode, Phone, Fax, Email, SupportRepId]
# Create a MySQL query for all customers in Texas named Jane

query = """
SELECT *
FROM customers
WHERE State = 'TX' AND FirstName = 'Jane'
"""

# open file test.json with pandas as df
df = pd.read_json('test.json')

# select top 10 orders from column order_value and sort by date column
df.sort_values(by='order_value', ascending=False).head(10)

def test(n):
    if n in {0, 1}:
        return n
    return test(n - 1) + test(n - 2)

# Explain what does test() do?

```


```
"""
SQL

table customer, columns=firstname, name, customer_id, address
table orders, columns=order_id, customer_id, product_id, product_amount
table products, columns=product_id, price, name, description

Write a query that returns the top 10 orders and show the customer name
"""
```