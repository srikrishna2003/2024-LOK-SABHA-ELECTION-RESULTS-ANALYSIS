import pandas as pd
import mysql.connector
import seaborn as sns
import matplotlib.pyplot as plt
import matplotlib.ticker as mticker

db_config = {
    'user': 'root',       
    'password': 'admin',   
    'host': 'localhost',           
    'database': 'election_data'    
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

# Fetch data
query1 = """
SELECT constituency, leading_candidate, leading_party, margin 
FROM election_results 
order by margin desc
limit 10
"""

cursor.execute(query1)

results = cursor.fetchall()

# Convert results to a DataFrame
df = pd.DataFrame(results, columns=['Constituency', 'Leading Candidate', 'Leading Party', 'Margin'])

# Close the cursor and connection
cursor.close()
conn.close()


df

df['Candidate and Party'] = df['Leading Candidate'] + ' (' + df['Leading Party'] + ')'

plt.figure(figsize=(14, 8))
sns.barplot(x='Margin', y='Candidate and Party', data=df, palette="viridis")
plt.title('Top 10 Candidates by Victory Margin')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')

ax = plt.gca()
ax.xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, _: '{:,.0f}'.format(x)))

plt.show()

db_config = {
    'user': 'root',       
    'password': 'admin',   
    'host': 'localhost',           
    'database': 'election_data'    
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query3 = """
SELECT constituency, leading_candidate, leading_party, margin 
FROM election_results 
order by margin asc
limit 10
"""

cursor.execute(query3)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['Constituency', 'Leading Candidate', 'Leading Party', 'Margin'])

cursor.close()
conn.close()

df

df['Candidate and Party'] = df['Leading Candidate'] + ' (' + df['Leading Party'] + ')'

plt.figure(figsize=(14, 8))
sns.barplot(x='Margin', y='Candidate and Party', data=df, palette="viridis")
plt.title('Bottom 10 Candidates by Victory Margin')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')

ax = plt.gca()
ax.xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, _: '{:,.0f}'.format(x)))

plt.show()

db_config = {
    'user': 'root',       
    'password': 'admin',   
    'host': 'localhost',           
    'database': 'election_data'    
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query3 = """
SELECT constituency, leading_candidate, leading_party, margin 
FROM election_results 
order by margin asc
limit 10
"""

cursor.execute(query3)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['Constituency', 'Leading Candidate', 'Leading Party', 'Margin'])

cursor.close()
conn.close()

df

df['Candidate and Party'] = df['Leading Candidate'] + ' (' + df['Leading Party'] + ')'

plt.figure(figsize=(14, 8))
sns.barplot(x='Margin', y='Candidate and Party', data=df, palette="viridis")
plt.title('Bottom 10 Candidates by Victory Margin')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')

ax = plt.gca()
ax.xaxis.set_major_formatter(mticker.FuncFormatter(lambda x, _: '{:,.0f}'.format(x)))

plt.show()

db_config = {
    'user': 'root',       # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',           # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'    # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query2 = """
select leading_party, COUNT(leading_party) as total_counts
from election_results
group by leading_party
"""

cursor.execute(query2)

results_query_2 = cursor.fetchall()

df_2 = pd.DataFrame(results_query_2, columns=['leading_party', 'Total Counts'])

cursor.close()
conn.close()

df_2

plt.figure(figsize=(14,14))
sns.barplot(x='Total Counts',y='leading_party',data=df_2,palette="viridis")
plt.title('Number of Constituencies Won by Each Party')
plt.xlabel('Number of Constituencies')
plt.ylabel('Leading Party')
plt.show()

db_config = {
    'user': 'root',       # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',           # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'    # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query4 = """
select trailing_party , SUM(margin) as sum
from election_results	
group by trailing_party
order by sum desc 
limit 10;
"""

cursor.execute(query4)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['trailing_party', 'count'])

cursor.close()
conn.close()

df


plt.figure(figsize=(12, 8))
sns.barplot(x='trailing_party', y='count', data=df)
plt.title('Top 10 Trailing Parties By Votes')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')
plt.xticks(rotation=45)
plt.show()

db_config = {
    'user': 'root',       # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',           # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'    # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query4 = """
select trailing_party , SUM(margin) as sum
from election_results	
group by trailing_party
order by sum desc 
limit 10;
"""

cursor.execute(query4)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['trailing_party', 'count'])

cursor.close()
conn.close()

df


plt.figure(figsize=(12, 8))
sns.barplot(x='trailing_party', y='count', data=df)
plt.title('Top 10 Trailing Parties By Votes')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')
plt.xticks(rotation=45)
plt.show()

db_config = {
    'user': 'root',       # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',           # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'    # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query4 = """
select trailing_party , COUNT(*) as sum
from election_results	
group by trailing_party
order by sum desc 
limit 10;
"""

cursor.execute(query4)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['trailing_party', 'count'])

cursor.close()
conn.close()

df


plt.figure(figsize=(12, 8))
sns.barplot(x='trailing_party', y='count', data=df)
plt.title('Top 10 Trailing Parties By Seats')
plt.xlabel('Margin')
plt.ylabel('Candidate and Party')
plt.xticks(rotation=45)
plt.show()

db_config = {
    'user': 'root',       # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',           # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'    # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query4 = """
WITH CTE AS (
    SELECT * 
    FROM election_results
    WHERE leading_candidate IN ('Rahul Gandhi', 'Narendra Modi', 'Amit Shah', 'Akhilesh Yadav')
)
SELECT
    constituency,
    leading_candidate,
    CAST(SUM(margin) AS FLOAT) AS Sum
FROM
    CTE
GROUP BY
    constituency,
    leading_candidate


"""

cursor.execute(query4)

results = cursor.fetchall()

df = pd.DataFrame(results, columns=['constituency','leading_candidate', 'sum'])

cursor.close()
conn.close()

df


plt.figure(figsize=(12, 8))
sns.barplot(x='leading_candidate', y='sum', hue='constituency', data=df)
plt.title('Comparison Of Votes For Top Party Candidates')
plt.xlabel('Candidate and Party')
plt.ylabel('Margin')
plt.xticks(rotation=45)

plt.legend(title='Constituency', bbox_to_anchor=(1.05, 1), loc='upper left')

plt.show()

db_config = {
    'user': 'root',        # Replace with your MySQL username
    'password': 'admin',   # Replace with your MySQL password
    'host': 'localhost',   # Replace with your MySQL host, e.g., 'localhost'
    'database': 'election_data'  # Replace with your database name
}

conn = mysql.connector.connect(**db_config)

cursor = conn.cursor()

query = """
SELECT
    margin
FROM
    election_results;
"""

cursor.execute(query)

results = cursor.fetchall()

cursor.close()
conn.close()

df = pd.DataFrame(results, columns=['margin'])


plt.figure(figsize=(10, 6))
plt.hist(df['margin'], bins=20, color='skyblue', edgecolor='black')
plt.title('Histogram of Margins of Victory')
plt.xlabel('Margin of Victory')
plt.ylabel('Frequency')
plt.grid(True)
plt.show()

