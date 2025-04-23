

<h1 align =center> IMPLEMENTATION OF EXACT INFERENCE METHOD OF BAYESIAN NETWORK </h1>
<H3> NAME: VINOD KUMAR S </H3>
<H3> REGISTER NUMBER: 212222240116 </H3>
<H3> EXPERIMENT NO: 02 </H3>
<H3> DATE: </H3>

## AIM:
To implement the inference Burglary P(B| j,⥗m) in alarm problem by using Variable Elimination method in Python.

## ALGORITHM:

### Step 1: 
Define the Bayesian Network structure for alarm problem with 5 random variables, Burglary,Earthquake,John Call,Mary Call and Alarm.<br>
### Step 2: 
Define the Conditional Probability Distributions (CPDs) for each variable using the TabularCPD class from the pgmpy library.<br>
### Step 3: 
Add the CPDs to the network.<br>
### Step 4: 
Initialize the inference engine using the VariableElimination class from the pgmpy library.<br>
### Step 5: 
Define the evidence (observed variables) and query variables.<br>
### Step 6: 
Perform exact inference using the defined evidence and query variables.<br>
### Step 7: 
Print the results.<br>

## PROGRAM:
```python
# Import required libraries
from pgmpy.models import BayesianNetwork
from pgmpy.factors.discrete import TabularCPD
from pgmpy.inference import VariableElimination

# Define bayesian network structure
network=BayesianNetwork([
    ('Burglary','Alarm'),
    ('Earthquake','Alarm'),
    ('Alarm','JohnCalls'),
    ('Alarm','MaryCalls')
])

# Define the conditional probability distributions
cpd_burglary = TabularCPD(variable='Burglary',variable_card=2,values=[[0.999],[0.001]])
cpd_earthquake = TabularCPD(variable='Earthquake',variable_card=2,values=[[0.998],[0.002]])
cpd_alarm = TabularCPD(variable ='Alarm',variable_card=2, values=[[0.999, 0.71, 0.06, 0.05],[0.001, 0.29, 0.94, 0.95]],evidence=['Burglary','Earthquake'],evidence_card=[2,2])
cpd_john_calls = TabularCPD(variable='JohnCalls',variable_card=2,values=[[0.95,0.1],[0.05,0.9]],evidence=['Alarm'],evidence_card=[2])
cpd_mary_calls = TabularCPD(variable='MaryCalls',variable_card=2,values=[[0.99,0.3],[0.01,0.7]],evidence=['Alarm'],evidence_card=[2])

# Add CPDs to the network
network.add_cpds(cpd_burglary,cpd_earthquake,cpd_alarm,cpd_john_calls,cpd_mary_calls)

# Initialize the inference engine
inference = VariableElimination(network)

# Perform exact inference-------1
evidence ={'JohnCalls':1,'MaryCalls':0} #john called(1) and mary didn't call (0) as evidence
query_variable ='Burglary'
result = inference.query(variables=[query_variable],evidence=evidence)

# Print result-----1
print(result)

# Perform exact inference--------2
evidence1 ={'JohnCalls':1,'MaryCalls':1} #john called(1) and mary called (1) as evidence
query_variable ='Burglary'
result2 = inference.query(variables=[query_variable],evidence=evidence)

# Print result-----2
print(result2)
```


## OUTPUT:
![image](https://github.com/user-attachments/assets/ec38dbf8-be24-48f8-a6b8-679c17a9fa5b)

![image](https://github.com/user-attachments/assets/67c3b379-e4d5-41fb-94c5-2db18dda815a)


## RESULT:
Thus, Bayesian Inference was successfully determined using the Variable Elimination Method.
