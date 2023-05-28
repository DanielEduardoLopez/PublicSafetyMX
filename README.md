<p align="center">
	<img src="Images/Header.png?raw=true" width=80% height=80%>
</p>

# Prediction of the Probability of Suffering Different Crimes in Mexico
#### By Daniel Eduardo López

**30/05/2023**

**[LinkedIn](https://www.linkedin.com/in/daniel-eduardo-lopez)**

**[Github](https://github.com/DanielEduardoLopez)**

____
### **Contents**

1. [Introduction](#intro)<br>
2. [General Objective](#objective)<br>
3. [Research Question](#question)<br>
4. [Hypothesis](#hypothesis)<br>
5. [Abridged Methodology](#methodology)<br>
6. [Results](#results)<br>
	6.1 [Data Collection](#collection)<br>
	6.2 [Data Exploration](#eda)<br>
	6.3 [Data Preparation](#preparation)<br>
	6.4 [Data Modeling](#modeling)<br>
	6.5 [Evaluation](#evaluation)<br>
7. [App](#app)<br>
8. [Conclusions](#conclusions)<br>
9. [Bibliography](#bibliography)<br>
10. [Description of Files in Repository](#files)<br>

____
<a class="anchor" id="intro"></a>
### **1. Introduction**

Since the 2000's, Mexico has experienced a sustained increase in crime and violence due to both criminal organizations and common criminals. In this sense, crime has become the top concern for the overall population [(Calderón, Heinle, Kuckertz, Rodríguez-Ferreira & Shirk, 2021)](#calderon). 

Some of the reasons for such a spread of crime and violence are the purposeful fragmentation of the criminal groups by the Mexican government, the consequent increase on competition and diversification among criminal organizations, a rampant corruption within the Mexican institutions, ineffective socio-economic policies, widespread impunity and low effective prosecution rates, and the alienation of local populations to criminals [(Felbab-Brown, 2019)](#calderon). 

In this context, it has been estimated that the crime rate was of 94.1 per 100,000 inhabitants before the COVID-19 lockdown in Mexico [(Balmori de la Miyar, Hoehn‑Velasco & Silverio‑Murillo, 2021)](#balmori).

However, the distribution of crime and violence is uneven accross the country. Thus, it is desirable to know how likely is suffering a crime based on the demographic and socio-economic profile of a given household/person, rather than just sticking to national or regional averages. 

Even though official crime data exists within the country, it has been estimated that the percentage of unreported crimes was of about 93.3% in 2020 [(Mexico Violence Resource Project, 2022)](#resource). In order to address this issue, the **National Survey of Victimization and Perception of Public Safety** (ENVIPE, by its acronym in Spanish) has been develop as a tool to gather representative data about the levels of crime incidence and unreported crimes -*cifra negra*- [(INEGI, 2021)](#inegi). 

Therefore, the ENVIPE data was used to train several classification models for the following crimes:
1. Total vehicle theft
2. Partial vehicle theft
3. Vandalism
4. Burglary
5. Kidnapping
6. Enforced disappearance
7. Murder
8. Theft
9. Other thefts
10. Bank fraud
11. Other frauds
12. Extortion
13. Threats
14. Injuries
15. Assault
16. Rape
17. Other crimes

This, in order to have a more accurate estimation of the probability of suffering different crimes in Mexico, according to an specific demographic and socio-economic profile.

___
<a class="anchor" id="objective"></a>
## **2. General Objective**

To predict the probability of suffering different crimes in Mexico based on demographic and socio-economic data.


___
<a class="anchor" id="question"></a>
## **3. Research Question**

What is the probability of suffering different crimes in Mexico based on demographic and socio-economic data?

___
<a class="anchor" id="hypothesis"></a>
## **4. Hypothesis**

The overall probability of suffering a crime in Mexico is about **0.094%** [(Balmori de la Miyar, Hoehn‑Velasco & Silverio‑Murillo, 2021)](#balmori). However, such probability is different according to the socioeconomic and demographic profile, with the low-income profiles having a higher probability of suffering crimes than the high-income profiles.

___
<a class="anchor" id="methodology"></a>
## **5. Abridged Methodology**

The methodology of the present study is based on Rollin’s *Foundational Methodology for Data Science* [(Rollins, 2015)](#rollins):

1. **Analytical approach**: Building and evaluation of a **multi-label classification model**.
2. **Data requirements**: Data about the incidence of the following crimes: Total vehicle theft, Partial vehicle theft, Vandalism, Burglary, Kidnapping, Enforced Disappearance, Murder, Theft, Other thefts, Bank fraud, Other frauds, Extortion, Threats, Injuries, Assault, Rape, and Other crimes; as well as data about the demographics and socio-economic conditions of the households/persons affected by those crimes.
3. **Data collection**: Data from ENVIPE was retrieved from the <a href="https://www.inegi.org.mx/programas/envipe/2022/#Datos_abiertos">INEGI's website</a>. Then, the different tables from ENVIPE were used to build a database in MySQL 8.0.32.0 (see the corresponding SQL script <a href="https://raw.githubusercontent.com/DanielEduardoLopez/PublicSafetyMX/main/sql_script.sql">here</a>). After that, said database was queried to gather only the relevant data and build the dataset to be used in the next steps (see the SQL query used <a href="https://raw.githubusercontent.com/DanielEduardoLopez/PublicSafetyMX/main/sql_query.sql">here</a>).
4. **Data exploration**: Data was explored with Python 3 and its libraries Numpy, Pandas, Matplotlib and Seaborn.
5. **Data preparation**: Data was cleaned and prepared with Python 3 and its libraries Numpy and Pandas.
6. **Data modeling**: The dataset was split in training, validation and testing sets. Then, a **multilayer perceptron (MLP) model** was built using Tensorflow and Keras. Sigmoid was used as the activation function for the output layer, whereas ReLU activation function was used for the hidden layers. Furthermore, the binary cross-entropy loss function and the Adam optimizer were used for the model compilation.
7. **Evaluation**: The model was primarily evaluated by means of the precision, recall, F1 score, and the area under the ROC curve (AUC ROC).
8. **Implementation**: An app was built and deployed with Streamlit.

___
<a class="anchor" id="results"></a>
## **6. Results**

### **6.1 Data Collection** <a class="anchor" id="collection"></a>

First, data from ENVIPE was retrieved from the <a href="https://www.inegi.org.mx/programas/envipe/2022/#Datos_abiertos">INEGI's website</a>, in form of several CSV files. 

Then, the encoding of the different original CSV files from INEGI were transformed to **UTF-8** using a <a href="https://github.com/DanielEduardoLopez/PublicSafetyMX/blob/45d5bae551ed9be40e30cd1a9578e45ddf3c69c0/CleanCSV.ipynb">previous notebook</a>. Furthermore, the datatypes of the different atributes were also adjusted.

Later, a database was built in MySQL 8.0.32.0 (see the corresponding SQL script <a href="https://raw.githubusercontent.com/DanielEduardoLopez/PublicSafetyMX/main/sql_script.sql">here</a>), comprising the following tables:
* tvivienda
* thogar 
* tsdem
* tmod_vic
* tper_vic1
* tper_vic2

The naming conventions from the original ENVIPE scheme were respected. 

The **ER Diagram** of the built database is as follows (obtained through the *Reverse Engineer* feature in MySQL Workbench):

<p align="center">
	<img src="Images/db_diagram.png?raw=true" width=70% height=60%>
</p>

After that, the UTF-8-encoded CSV files with all the survey observations were loaded to their correspondent tables in the database.

Finally, after a thorough review of all the atributes in each of the tables of the schema, the database was queried to gather only the relevant data and build the dataset to be used in this notebook (see the SQL query used <a href="https://raw.githubusercontent.com/DanielEduardoLopez/PublicSafetyMX/main/sql_query.sql">here</a>).


### **6.2 Data Exploration** <a class="anchor" id="eda"></a>

The dataset comprised 84 columns with **202,504 observations**.

#### **Description of attributes in dataset**

The **description of each of the attributes** in the dataset is as follows:

| Attribute | Description (English)                                                                               | Description (Spanish)                                                                                         |
|------------------------------------|-----------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| HousingClass                       | Housing type                                                                                        | Tipo de vivienda                                                                                              |
| PeopleHousehold                    | Number of people living in the home                                                                 | Número de personas viviendo en la vivienda                                                                    |
| Kinship                            | Relationship with the head of the household                                                         | Parentesco con el jefe del hogar                                                                              |
| Education                          | Education                                                                                           | Educación                                                                                                     |
| Activity                           | Activity                                                                                            | Actividad                                                                                                     |
| Job                                | Job                                                                                                 | Trabajo                                                                                                       |
| Crime                              | Type of crime                                                                                       | Tipo de delito                                                                                                |
| Sex                                | Sex                                                                                                 | Género                                                                                                        |
| Age                                | Age                                                                                                 | Edad                                                                                                          |
| MetroArea                          | Metropolitan area of occurrence of the crime                                                        | Area metropolitana de ocurrencia del delito                                                                   |
| Month                              | Month of occurrence of the crime                                                                    | Mes de ocurrencia del delito                                                                                  |
| State                              | State of occurrence of the crime                                                                    | Estado de ocurrencia del delito                                                                               |
| Municipality                       | Municipality of occurrence of the crime                                                             | Municipio de ocurrencia del delito                                                                            |
| Hour                               | Crime occurrence time                                                                               | Hora de ocurrencia del delito                                                                                 |
| Place                              | Place of occurrence of the crime                                                                    | Lugar de ocurrencia del delito                                                                                |
| Category                           | Urban-Rural                                                                                         | Urbano-Rural                                                                                                  |
| SocialClass                        | Socioeconomic stratum                                                                               | Estrato socioeconómico                                                                                        |
| InhabitingTime                     | Time living in the house                                                                            | Tiempo habitando en la vivienda                                                                               |
| StopGoingOutNight                  | Stop going out at night for fear of being a victim                                                  | Dejar de salir de noche por temor a ser víctima                                                               |
| StopChildrenAlone                  | Stop allowing minors to go out alone for fear of being a victim                                     | Dejar de permitir a menores salir solos por temor a ser víctima                                               |
| StopVisitingFamily                 | Stop visiting relatives or friends for fear of being a victim                                       | Dejar de visitar parientes o amigos por temor a ser víctima                                                   |
| StopTakingTaxis                    | Stop taking a taxi for fear of being a victim                                                       | Dejar de tomar taxi por temor a ser víctima                                                                   |
| StopTakingPublicTransit            | Stop using public transport for fear of being a victim                                              | Dejar de usar transporte público por temor a ser víctima                                                      |
| StopCarryingCash                   | Stop carrying cash for fear of being a victim                                                       | Dejar de llevar dinero en efectivo por temor a ser víctima                                                    |
| StopGoingSchool                    | Stop going to school for fear of being a victim                                                     | Dejar de ir a la escuela por temor a ser víctima                                                              |
| StopGoingCinema                    | Stop going to the movies or theater for fear of being a victim                                      | Dejar de ir al cine o teatro por temor a ser víctima                                                          |
| StopWalking                        | Stop going for a walk for fear of being a victim                                                    | Dejar de salir a caminar por temor a ser víctima                                                              |
| StopWearingJewels                  | Stop wearing jewelry for fear of being a victim                                                     | Dejar de usar joyas por temor a ser víctima                                                                   |
| StopEatingOut                      | Stop going out for lunch or dinner for fear of being a victim                                       | Dejar de salir a comer o cenar por temor a ser víctima                                                        |
| StopCreditCard                     | Stop carrying a credit or debit card for fear of being a victim                                     | Dejar de llevar tarjeta de crédito o débito por temor a ser víctima                                           |
| StopStadium                        | Stop going to the stadium for fear of being a victim                                                | Dejar de ir al estadio por temor a ser víctima                                                                |
| StopSupermart                      | Stop going to shopping malls for fear of being a victim                                             | Dejar de frecuentar centros comerciales por temor a ser víctima                                               |
| StopHighways                       | Stop traveling by road for fear of being a victim                                                   | Dejar de viajar por carretera por temor a ser víctima                                                         |
| StopMobilePhones                   | Stop carrying a mobile or cell phone for fear of being a victim                                     | Dejar de llevar teléfono móvil o celular por temor a ser víctima                                              |
| ProtectionDoorsWindows             | Crime protection measures: changing doors or windows                                                | Medidas de protección contra delincuencia: cambiar puertas o ventanas                                         |
| ProtectionLocks                    | Crime Protection Measures: change or place locks and/or padlocks                                    | Medidas de protección contra delincuencia: cambiar o colocar cerraduras y/o candados                          |
| ProtectionFences                   | Crime Protection Measures: place or reinforce bars or fences                                        | Medidas de protección contra delincuencia: colocar o reforzar rejas o bardas                                  |
| ProtectionAlarmsVideo              | Crime Protection Measures: install alarms and/or surveillance video cameras                         | Medidas de protección contra delincuencia: instalar alarmas y/o videocámaras de vigilancia                    |
| ProtectionPrivateSurveillance      | Crime Protection Measures: hire private surveillance in the street or neighborhood                  | Medidas de protección contra delincuencia: contratar vigilancia privada en la calle o colonia                 |
| ProtectionNeighbors                | Crime Protection Measures: carry out joint actions with your neighbors                              | Medidas de protección contra delincuencia: realizar acciones conjuntas con sus vecinos                        |
| ProtectionInsurance                | Crime Protection Measures: take out insurance                                                       | Medidas de protección contra delincuencia: contratar seguros                                                  |
| ProtectionDog                      | Crime Protection Measures: Buying a Watchdog                                                        | Medidas de protección contra delincuencia: comprar un perro guardián                                          |
| ProtectionWeapons                  | Crime Protection Measures: acquiring firearms                                                       | Medidas de protección contra delincuencia: adquirir armas de fuego                                            |
| ProtectionMoving                   | Crime Protection Measures: changing your home or place of residence                                 | Medidas de protección contra delincuencia: cambiarse de vivienda o lugar de residencia                        |
| ProtectionOther                    | Crime Protection Measures: Other measure                                                            | Medidas de protección contra delincuencia: Otra medida                                                        |
| ProtectionExpenses                 | Expenses in protection against crime                                                                | Gastos en protección contra delincuencia                                                                      |
| Automobiles                        | Car, van or truck owner household                                                                   | Hogar propietario de automóvil, camioneta o camión                                                            |
| NumberAutomobiles                  | Number of vehicles (cars, vans, or trucks) owned by the household                                   | Número de vehículos (automóviles, camionetas o camiones) propiedad del hogar                                  |
| CrimeVehicleTheft                  | Home victim of total vehicle theft                                                                  | Hogar víctima de robo total de vehículo                                                                       |
| NumberVehicleThefts                | Number of times home victim of total vehicle theft                                                  | Número de veces hogar víctima de robo total vehículo                                                          |
| CrimePartialVehicleTheft           | Home victim of partial vehicle theft                                                                | Hogar víctima de robo parcial de vehículo                                                                     |
| NumberPartialVehicleThefts         | Number of times home victim of partial vehicle theft                                                | Número de veces hogar víctima de robo parcial vehículo                                                        |
| CrimeVandalism                     | Home victim of graffiti or vandalism                                                                | Hogar víctima de grafiti o vandalismo                                                                         |
| NumberVandalisms                   | Number of times home victim of graffiti or vandalism                                                | Número de veces hogar víctima de grafiti o vandalismo                                                         |
| CrimeBurglary                      | Home victim of home-room robbery                                                                    | Hogar víctima de robo a casa                                                                                  |
| NumberBurglaries                   | Number of times home victim of burglary                                                             | Número de veces hogar víctima de robo a casa                                                                  |
| CrimeFamilyKidnapping              | Household victim of kidnapping                                                                      | Hogar víctima de secuestro                                                                                    |
| NumberFamilyKidnappings            | Number of members victims of kidnapping                                                             | Número de integrantes víctimas de secuestro                                                                   |
| CrimeFamilyEnforcedDisappearance   | Household victim of enforced disappearance                                                          | Hogar víctima de desaparición forzada                                                                         |
| NumberFamilyEnforcedDisappearances | Number of members victims of forced disappearance                                                   | Número de integrantes víctimas de desaparición forzada                                                        |
| CrimeFamilyMurder                  | Household victim of homicide                                                                        | Hogar víctima de homicidio                                                                                    |
| NumberMurders                      | Number of members victims of homicide                                                               | Número de integrantes víctimas de homicidio                                                                   |
| CrimeTheft                         | Robbery or assault victim                                                                           | Víctima de robo o asalto                                                                                      |
| NumberThefts                       | Number of times victim of robbery or assault                                                        | Número de veces víctima de robo o asalto                                                                      |
| CrimeOtherTheft                    | Robbery victim in a different form                                                                  | Víctima de robo en forma distinta                                                                             |
| NumberOtherThefts                  | Number of times victim of robbery in a different way                                                | Número de veces víctima de robo en forma distinta                                                             |
| CrimeBankFraud                     | Bank fraud victim                                                                                   | Víctima de fraude bancario                                                                                    |
| NumberBankFrauds                   | Number of times victim of fraud                                                                     | Número de veces víctima de fraude                                                                             |
| CrimeFraud                         | Consumer Fraud Victim                                                                               | Víctima de fraude al consumidor                                                                               |
| NumberFrauds                       | Number of times victim of consumer fraud                                                            | Número de veces víctima de fraude al consumidor                                                               |
| CrimeExtortion                     | Extortion victim                                                                                    | Víctima de extorsión                                                                                          |
| NumberExtortions                   | Number of times extortion victim                                                                    | Número de veces víctima de extorsión                                                                          |
| CrimeThreats                       | Victim of threats                                                                                   | Víctima de amenazas                                                                                           |
| NumberThreats                      | Number of times victim of threats                                                                   | Número de veces víctima de amenazas                                                                           |
| CrimeInjuries                      | Injury victim                                                                                       | Víctima de lesiones                                                                                           |
| NumberInjuries                     | Number of times victim of injuries                                                                  | Número de veces víctima de lesiones                                                                           |
| CrimeKidnapping                    | Kidnapping victim                                                                                   | Víctima de secuestro                                                                                          |
| NumberKidnappings                  | Number of times kidnapped                                                                           | Número de veces víctima de secuestro                                                                          |
| CrimeAssault                       | Victim of sexual harassment or intimidation, groping, indecent exposure, attempted rape             | Víctima de hostigamiento o intimidación sexual, manoseo, exhibicionismo, intento de violación                 |
| NumberAssaults                     | Number of times victim of sexual harassment or intimidation, groping, exhibitionism, attempted rape | Número de veces víctima de hostigamiento o intimidación sexual, manoseo, exhibicionismo, intento de violación |
| CrimeRape                          | Rape victim                                                                                         | Víctima de violación sexual                                                                                   |
| NumberRapes                        | Number of times rape victim                                                                         | Número de veces víctima de violación sexual                                                                   |
| CrimeOther                         | Victim of other crimes                                                                              | Víctima de otros delitos                                                                                      |
| NumberOther                        | Number of times victim of other crimes                                                              | Número de veces víctima de otros delitos                                                                      |


### **Values encoding of the categorical attributes in dataset**

The encoding of the values for each categorical attribute according to [(INEGI, 2021)](#inegi), is as follows:

* **HousingClass**: 

Value | Description (English) | Description (Spanish)
--- | --- | ---
1 | Stand-alone house  | Casa independiente
2 | Apartment in building | Departamento en edificio
3 | *Vecindad* | Vivienda en vecindad
4 | Rooftop room housing | Vivienda en cuarto de azotea
5 | Premises not built for housing | Local no construido para habitación

* **Kinship**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
1 | Household head  | Jefe(a)
2 | Spouse | Esposo(a) 
3 | Child | Hijo(a)
4 | Parent | Padre o madre
5 | Other relationship: uncle, nephew, cousin | Otro parentesco: tío(a), sobrino(a), primo(a)
6 | No relationship | Sin parentesco

* **Education**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
0 | None  | Ninguno
1 | Preschool  | Preescolar
2 | Elementary | Primaria
3 | Secondary | Secundaria
4 | Technical career with finished secondary school | Carrera técnica con secundaria terminada
5 | Basic normal (with background in secondary) | Normal básica (con antecedente en secundaria)
6 | High School | Preparatoria o bachillerato
7 | Technical career with finished high school | Carrera técnica con preparatoria terminada
8 | Bachelor or professional | Licenciatura o profesional
9 | Master's or PhD | Maestría o doctorado
99 | Unspecified level | Nivel no especificado

* **Activity**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
1 | Worker  | Trabajador
2 | Had a job, but didn't work | Tenía trabajo pero no trabajó
3 | Looking for a job | En busca de trabajo
4 | Student | Estudiante
5 | Housekeeper | Dedicado a los quehaceres del hogar
6 | Retired or pensioner | Jubilado(a) o pensionado(a)
7 | Permanently disabled from working | Incapacitado(a) permanentemente para trabajar
8 | Didn't work | No trabajó
9 | Not specified | No especificado

* **Job**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
1 | Laborer or pawn  | Jornalero(a) o peón
2 | Employee or worker | Empleado(a) u obrero(a)
3 | Self-employed worker (does not hire workers) | Trabajador(a) por su cuenta (no contrata trabajadores)
4 | Boss or employer (hires workers) | Patrón(a) o empleador(a)? (contrata trabajadores)
5 | Unpaid worker | Trabajador(a) sin pago

* **Crime**:

| Value  | Description (English)                                                                                                                                                        | Description (Spanish)                                                                                                                                                         |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1<br>  | Total vehicle theft (car, van, truck)                                                                                                                                        | Robo total de vehículo (automóvil, camioneta, camión)                                                                                                                         |
| 2<br>  | Theft of vehicle accessories, spare parts or tools (car, van, truck)                                                                                                         | Robo de accesorios, refacciones o herramientas de vehículos (automóvil, camioneta, camión)                                                                                    |
| 3<br>  | Fence painting or graffiti on your home, intentional scratches on your vehicle, or other types of vandalism                                                                  | Pinta de barda o grafiti en su casa, rayones intencionales en su vehículo u otro tipo de vandalismo                                                                           |
| 4<br>  | Someone entered your home or apartment without permission using force or deceit and stole or attempted to steal something                                                    | Alguien entró a su casa o departamento sin permiso mediante el uso de la fuerza o por engaños y robó o intentó robar algo                                                     |
| 5<br>  | Robbery or assault on the street or on public transport (includes bank or ATM robbery)                                                                                       | Robo o asalto en la calle o en el transporte público (incluye robo en banco o cajero automático)                                                                              |
| 6<br>  | Theft in a manner other than the above                                                                                                                                       | Robo en forma distinta a la anterior                                                                                                                                          |
| 7<br>  | Someone used your checkbook, card number, or bank account without your permission to charge or withdraw money from your accounts (bank fraud), or gave you counterfeit money | Alguien usó su chequera, número de tarjeta o cuenta bancaria sin su permiso para realizar cargos o para extraer dinero de sus cuentas (fraude bancario) o le dio dinero falso |
| 8<br>  | You gave money for a product or service that you did not receive as agreed (consumer fraud)                                                                                  | Entregó dinero por un producto o un servicio que no recibió conforme a lo acordado (fraude al consumidor)                                                                     |
| 9<br>  | Threats, pressure or tricks to demand money or property; or to make him do something or stop doing it (extortion)                                                            | Amenazas, presiones o engaños para exigirle dinero o bienes; o para que hiciera algo o dejara de hacerlo (extorsión)                                                          |
| 10<br> | Verbal threats from someone who is fully identified or in writing towards you saying that they are going to cause harm to you, your family, your property or your job        | Amenazas verbales de alguien plenamente identificado o por escrito hacia su persona diciendo que le va a causar un daño a usted, a su familia, a sus bienes o su trabajo      |
| 11<br> | Someone hit you just because of an abusive attitude or because of an argument, causing physical injury (bruises, fractures, cuts, etc.)                                      | Alguien sólo por actitud abusiva o por una discusión lo(a) golpeó generándole una lesión física (moretones, fracturas, cortadas, etc.)                                        |
| 12<br> | They kidnapped you to demand money or goods                                                                                                                                  | Lo secuestraron para exigir dinero o bienes                                                                                                                                   |
| 13<br> | Someone against your will assaulted you by sexual harassment or intimidation, groping, indecent exposure, or attempted rape                                                  | Alguien en contra de su voluntad lo(a) agredió mediante hostigamiento o intimidación sexual, manoseo, exhibicionismo o intento de violación                                   |
| 14<br> | Was forced by physical violence or threat by someone known or unknown to engage in unwanted sexual activity (sexual rape)                                                    | Fue obligado(a) mediante violencia física o amenaza por alguien conocido o desconocido a tener una actividad sexual no deseada (violación sexual)                             |
| 15<br> | Other crimes different from the previous ones                                                                                                                                | Otros delitos distintos a los anteriores                                                                                                                                      |
| A<br>  | Complete interview with victimization     

* **Sex**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
1 | Male  | Hombre
2 | Female | Mujer

* **MetroArea**:

| Value  | Description      |
| ------ | ---------------- |
| 1<br>  | Ciudad de México |
| 2<br>  | Guadalajara      |
| 3<br>  | Monterrey        |
| 4<br>  | Puebla           |
| 5<br>  | León             |
| 6<br>  | La Laguna        |
| 7<br>  | San Luis Potosí  |
| 8<br>  | Mérida           |
| 9<br>  | Chihuahua        |
| 10<br> | Tampico          |
| 12<br> | Veracruz         |
| 13<br> | Acapulco         |
| 14<br> | Aguascalientes   |
| 15<br> | Morelia          |
| 16<br> | Toluca           |
| 17<br> | Saltillo         |
| 18<br> | Villahermosa     |
| 19<br> | Tuxtla Gutiérrez |
| 21<br> | Tijuana          |
| 24<br> | Culiacán         |
| 25<br> | Hermosillo       |
| 26<br> | Durango          |
| 27<br> | Tepic            |
| 28<br> | Campeche         |
| 29<br> | Cuernavaca       |
| 31<br> | Oaxaca           |
| 32<br> | Zacatecas        |
| 33<br> | Colima           |
| 36<br> | Querétaro        |
| 39<br> | Tlaxcala         |
| 40<br> | La Paz           |
| 41<br> | Cancún           |
| 43<br> | Pachuca          |

* **Month**:

| Value  | Description (English)     | Description (Spanish) |
| ------ | ------------------------- | --------------------- |
| 1<br>  | January                   | Enero                 |
| 2<br>  | February                  | Febrero               |
| 3<br>  | March                     | Marzo                 |
| 4<br>  | April                     | Abril                 |
| 5<br>  | May                       | Mayo                  |
| 6<br>  | June                      | Junio                 |
| 7<br>  | July                      | Julio                 |
| 8<br>  | August                    | Agosto                |
| 9<br>  | September                 | Septiembre            |
| 10<br> | October                   | Octubre               |
| 11<br> | November                  | Noviembre             |
| 12<br> | December                  | Diciembre             |
| 99<br> | Didn't know/Didn't answer | No sabe / no responde |

* **State**:

| Value  | Description                        |
| ------ | ---------------------------------- |
| 1<br>  | Aguascalientes                     |
| 2<br>  | Baja California                    |
| 3<br>  | Baja California Sur                |
| 4<br>  | Campeche                           |
| 5<br>  | Coahuila                           |
| 6<br>  | Colima                             |
| 7<br>  | Chiapas                            |
| 8<br>  | Chihuahua                          |
| 9<br>  | Ciudad de México                   |
| 10<br> | Durango                            |
| 11<br> | Guanajuato                         |
| 12<br> | Guerrero                           |
| 13<br> | Hidalgo                            |
| 14<br> | Jalisco                            |
| 15<br> | Estado de México                   |
| 16<br> | Michoacán de Ocampo                |
| 17<br> | Morelos                            |
| 18<br> | Nayarit                            |
| 19<br> | Nuevo León                         |
| 20<br> | Oaxaca                             |
| 21<br> | Puebla de Zaragoza                 |
| 22<br> | Querétaro                          |
| 23<br> | Quintana Roo                       |
| 24<br> | San Luis Potosí                    |
| 25<br> | Sinaloa                            |
| 26<br> | Sonora                             |
| 27<br> | Tabasco                            |
| 28<br> | Tamaulipas                         |
| 29<br> | Tlaxcala                           |
| 30<br> | Veracruz Llave                     |
| 31<br> | Yucatán                            |
| 32<br> | Zacatecas                          |
| 99<br> | Entidad federativa no especificada |


* **Municipality**:

| Value  | Description                        |
| ------ | ---------------------------------- |
| 1…570  | Municipality number                    |
| 999  | Not specified                   |

* **Hour**:

| Values | Description (English)                               | Description (Spanish)                  |
| ------ | --------------------------------------------------- | -------------------------------------- |
| 1<br>  | In the morning (from 6:01 a.m. to 12:00 p.m.)       | En la mañana (de 6:01 a 12:00 hrs.)    |
| 2<br>  | In the afternoon (from 12:01 a.m. to 6:00 p.m.)     | En la tarde (de 12:01 a 18:00 hrs.)    |
| 3<br>  | At night (from 6:01 p.m. to 12:00 a.m.)             | En la noche (de 18:01 a 24:00 hrs.)    |
| 4<br>  | In the early morning (from 12:01 a.m. to 6:00 a.m.) | En la madrugada (de 00:01 a 6:00 hrs.) |
| 9<br>  | Didn't know / Didn't answer                         | No sabe / no responde                  |

* **Place**:

| Value | Description (English)          | Description (Spanish)           |
| ----- | ------------------------------ | ------------------------------- |
| 1<br> | In the street                  | En la calle                     |
| 2<br> | At home                        | En su casa                      |
| 3<br> | In the workplace               | En su trabajo                   |
| 4<br> | In a business or establishment | En un negocio o establecimiento |
| 5<br> | In a public place              | En un lugar público             |
| 6<br> | In the public transportation   | En el transporte público        |
| 7<br> | In a highway                   | En una carretera                |
| 8<br> | Other                          | Otro                            |
| 9<br> | Didn't know / Didn't answer    | No sabe / no responde           |

* **Category**:

Value | Description (English) | Description (Spanish)
--- | --- | ---
U | Urban | Urbano
C | Urban complement | Complemento urbano
R | Rural | Rural

* **SocialClass**:

| Value | Description (English) | Description (Spanish) |
| ----- | --------------------- | --------------------- |
| 1<br> | Low income            | Bajo                  |
| 2<br> | Lower middle income   | Medio bajo            |
| 3<br> | Higher middle income  | Medio alto            |
| 4<br> | High income           | Alto                  |

* **InhabitingTime**:

| Value | Description (English)         | Description (Spanish)     |
| ----- | ----------------------------- | ------------------------- |
| 1<br> | Less than six months          | Menos de seis meses       |
| 2<br> | Between six months and a year | Entre seis meses y un año |
| 3<br> | More than a year              | Más de un año             |
| 9<br> | Didn't know / Didn't answer   | No sabe / no responde     |

On the other hand, the rest of attributes in the dataset have the following nomenclature:

| Value | Description (English)       | Description (Spanish) |
| ----- | --------------------------- | --------------------- |
| 1<br> | Yes                         | Sí                    |
| 2<br> | No                          | No                    |
| 3<br> | Not applicable              | No aplica             |
| 9<br> | Didn't know / Didn't answer | No sabe / no responde |


### **Data Quality**

**No missing values** were detected in the dataset. So, it was not necessary to perform filtering or imputation. 

Furthermore, the dataset was also free from **outliers**.

### **Exploratory Data Analysis**

In this section, the data was explored. Nonetheless, as many attributes are present at the dataset, only some of them were analyzed in detail.

Most of the surveyed people lived on **stand-alone houses**.

<p align="center">
	<img src="Images/Fig_HousingClassFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Most of the respondents to the survey were **female**.

<p align="center">
	<img src="Images/Fig_SexFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Most of the respondents were from 18 to 34 years old.

<p align="center">
	<img src="Images/Fig_AgeFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Furthermore, most of the respondents held a **secondary certificate** or a **bachelor degree**.

<p align="center">
	<img src="Images/Fig_EducationFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Moreover, most of the people surveyed were **workers or employees**.

<p align="center">
	<img src="Images/Fig_JobCategoryFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Most of the crime observations in the survey came from the center of Mexico, in particular, **Ciudad de México, Puebla and Querétaro**.

<p align="center">
	<img src="Images/Fig_StateFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

And, as expectable, most of the crime observations comes from the **Greater Mexico City** area.

<p align="center">
	<img src="Images/Fig_MetropolitanAreaFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Moreover, the municipalities of **Querétaro** in the State of Querétaro, and **Puebla** in the State of Puebla were the ones with the largest number of observations in the survey. This result is consistent with the number of observations per state shown above.

<p align="center">
	<img src="Images/Fig_MunicipalityFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Most of the observations in the survey were drawn from **lower middle income** stratums.

<p align="center">
	<img src="Images/Fig_SocialClassFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

On the other hand, regarding the crimes, **theft of vehicle spare parts** is the most common crime in the dataset.

<p align="center">
	<img src="Images/Fig_CrimeFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Interestingly, most of the crimes in the dataset were committed on **December**.

<p align="center">
	<img src="Images/Fig_MonthFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Moreover, most of the crimes were committed in the **afternoon** or at **night**.

<p align="center">
	<img src="Images/Fig_HouroftheDayFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Shockingly, most of the crimes were commited either **at home or in the street**.

<p align="center">
	<img src="Images/Fig_PlaceFrequencyPlot.png?raw=true" width=80% height=80%>
</p>

Noteworthy, about **24%** of the surveyed people were victims of **partial vehicle theft**. Or, in other words, about a quarter of the people have suffered the theft of spare parts from their vehicles.

<p align="center">
	<img src="Images/Fig_PartialVehicleTheftDonutChart.png?raw=true" width=60% height=60%>
</p>

Whereas about **5%** of the surveyed people were victims of **total vehicle theft**.

<p align="center">
	<img src="Images/Fig_TotalVehicleTheftDonutChart.png?raw=true" width=60% height=60%>
</p>

About **19%** of the surveyed people have suffered of **vandalism** in their properties.

<p align="center">
	<img src="Images/Fig_VandalismDonutChart.png?raw=true" width=60% height=60%>
</p>

Shockingly, about **17%** of the households have been victims of **burglary**, according to the survey.

<p align="center">
	<img src="Images/Fig_BurglaryDonutChart.png?raw=true" width=60% height=60%>
</p>

About **17%** of the surveyed people have been victims of **theft**.

<p align="center">
	<img src="Images/Fig_TheftDonutChart.png?raw=true" width=60% height=60%>
</p>

According to the survey, about **3%** of the families have been victims of **kidnapping**.

<p align="center">
	<img src="Images/Fig_KidnappingDonutChart.png?raw=true" width=60% height=60%>
</p>

Again, according to the survey, about **2%** of the families in México had a member that was victim of **enforced dissappearence**.

<p align="center">
	<img src="Images/Fig_EnforcedDisappearanceDonutChart.png?raw=true" width=60% height=60%>
</p>

In view of the chart above, about **2%** of the Mexican families have been victim of a **murder** crime.

<p align="center">
	<img src="Images/Fig_MurderDonutChart.png?raw=true" width=60% height=60%>
</p>

According to the dataset, about **1%** of surveyed people have been victims of **rape**.

<p align="center">
	<img src="Images/Fig_RapeDonutChart.png?raw=true" width=60% height=60%>
</p>

Please refer to the **[notebook](https://github.com/DanielEduardoLopez/CrimePredictionMX/blob/main/CrimePredictionMX.ipynb)** for the full set of charts for all the crimes.


### **6.3 Data Preparation** <a class="anchor" id="preparation"></a>

Pending...


### **6.4 Modeling** <a class="anchor" id="modeling"></a>

Pending...


### **6.5 Evaluation** <a class="anchor" id="evaluation"></a>

Pending...

___
<a class="anchor" id="app"></a>
## **7. App**

Pending...

___
<a class="anchor" id="conclusions"></a>
## **8. Conclusions**

Pending...

___
<a class="anchor" id="bibliography"></a>
## **9. Bibliography**

* <a class="anchor" id="balmori"></a> **Balmori de la Miyar, J. R., Hoehn‑Velasco, L. & Silverio‑Murillo, A. (2021).** The U‑shaped crime recovery during COVID‑19 evidence from national crime rates in Mexico. *Crime Science*. 10:14. https://doi.org/10.1186/s40163-021-00147-8
* <a class="anchor" id="calderon"></a> **Calderón, L. Y., Heinle, K., Kuckertz, R. E., Rodríguez-Ferreira, O. & Shirk, D. A. (eds.) (2021).** *Organized Crime and Violence in Mexico: 2021 Special Report*. Justice in Mexico, University of San Diego. https://justiceinmexico.org/wp-content/uploads/2021/10/OCVM-21.pdf 
* <a class="anchor" id="felbab"></a> **Felbab-Brown, V. (2019).** *Mexico’s out-of-control criminal market*. Brookings Institution. https://www.brookings.edu/wp-content/uploads/2019/03/FP_20190322_mexico_crime-2.pdf 
* <a class="anchor" id="inegi"></a> **INEGI (2022).** *Encuesta Nacional de Victimización y Percepción sobre Seguridad Pública (ENVIPE) 2022*. https://www.inegi.org.mx/programas/envipe/2022/
* <a class="anchor" id="resource"></a> **Mexico Violence Resource Project (2022).** *Essential Numbers*. UC San Diego’s Center for U.S.-Mexican Studies. https://www.mexicoviolence.org/essential-numbers
* <a class="anchor" id="rollins"></a> **Rollins, J. B. (2015)**. *Metodología Fundamental para la Ciencia de Datos. Somers: IBM Corporation.* https://www.ibm.com/downloads/cas/WKK9DX51

___
<a class="anchor" id="files"></a>
## **10. Description of files in repository**
File | Description 
--- | --- 
CleanCSV.ipynb | Notebook with the Python code for encoding the original CSV files from INEGI into UTF-8.
PublicSafetyMX.ipynb | Notebook with the Python code for exploring, wrangling, modeling, and evaluating the crime data.
dataset.csv.csv | Queried data retrieved from the database with the data from ENVIPE.
sql_query.sql | SQL code for generating the dataset.
sql_script.sql| SQL script to build database with the data from ENVIPE.
