# Python Data Type Notes

### Dictionaries

To create a dictionary use curly braces {}



#### Loop using dictionaries

```Python
counties_dict = {"Arapahoe": 422829, "Denver": 463353, "Jefferson": 432438}

#will provide keys
for county in counties_dict:
    print(county)

for county in counties_dict.keys():
    print(county)

# will provide values
for voters in counties_dict.values():
    print(voters)

# will provide the key value pairs
for key, value in counties_dict.items():
    print(key, value)

# can also use any word for variables
for county, voters in counties_dict.items():
    print(str(county) + " county has " + str(voters) + " voters."

voting_data = [{"county":"Arapahoe", "registered_voters": 422829},
                {"county":"Denver", "registered_voters": 463353},
                {"county":"Jefferson", "registered_voters": 432438}]

# loops through list of dictionaries and displays specific value
for county_dict in voting_data:
    print(county_dict['registered_voters'])
```

### Printing Formats

print("string")
print('string' + str(int) + 'string')

####F strings
Can be used instead of concatenation. Curly braces are used to insert variable into text

```python
counties_dict = {"Arapahoe": 369237, "Denver":413229, "Jefferson": 390222}

for county, voters in counties_dict.items():
    print(f"{county} county has {voters} registered voters.")
```

#### Multiline F strings

```python
candidate_votes = int(input("How many votes did the candidate get in the election? "))
total_votes = int(input("What is the total number of votes in the election? "))
message_to_candidate = (
    f"You received {candidate_votes} number of votes. "
    f"The total number of votes in the election was {total_votes}. "
    f"You received {candidate_votes / total_votes * 100}% of the total votes.")

print(message_to_candidate)
```

There is no delimiter between f strings.

#### Floating point formatting
With numeric values you can add the formatting in the F string itself.
For a comma thousand separator use this: {value:,}
For a floating point, you add .f or 2f and so on  e.g. {value:,.2f}

Printing values from a list of dictionaries:

```python
voting_data = [{"county":"Arapahoe", "registered_voters": 422829},
{"county":"Denver", "registered_voters": 463353},
{"county":"Jefferson", "registered_voters": 432438}]

for dictionary in voting_data:
    print(f"{dictionary['county']} county has {dictionary['registered_voters']:,} registered voters")
```

### Importing data


###Final product of analysis

```python
# the data we need to retrieve
import os
import csv
# assign variables for the file to load and the path as well as to save
file_to_load = os.path.join('Resources','election_results.csv')
file_to_save = os.path.join('Analysis', 'election_results.txt')

# initialize vote counter
total_votes = 0
# initialize list of candidate names
candidate_options = []
#initialize dictionary to store candidate votes
candidate_votes = {}

#initialize arrays for winning candidate
winning_candidate = ""
winning_count = 0
winning_percentage = 0

# open the election results and read the file
with open(file_to_load) as election_data:
  #To-do: read and analyze data here
    file_reader = csv.reader(election_data)
    headers = next(file_reader)

    for row in file_reader:

      #t his adds up all of the votes
        total_votes += 1
        candidate_name = row[2]
        if candidate_name not in candidate_options:

          #this adds a candidate's name to the list
          candidate_options.append(candidate_name)

          #this sets up arrays for each candidate and sets them to zero
          candidate_votes[candidate_name] = 0

          # this tallies votes for each candidate
        candidate_votes[candidate_name] += 1

with open(file_to_save, "w") as txt_file:
    # Print the final vote count to the terminal.
    election_results = (
        f"\nElection Results\n"
        f"-------------------------\n"
        f"Total Votes: {total_votes:,}\n"
        f"-------------------------\n")
    print(election_results, end="")
    # Save the final vote count to the text file.
    txt_file.write(election_results)

    # the total number of votes cast
    #print(total_votes)

    # A complete list of candidates who received votes
    #print(candidate_options)
    #print(candidate_votes)

    # The percentage of votes each candidate won
    # iterate through candidate list
    for candidate in candidate_votes:
        # retrieve number of votes for each candidate
        votes = candidate_votes[candidate]

        # calculate the percentage of vote
        vote_percentage = int(votes)/int(total_votes) * 100

        # print the candidate name and vote count
        candidate_results = (
            f"{candidate}: {vote_percentage:.1f}% ({votes:,})\n")

        print(candidate_results)

        txt_file.write(candidate_results)

        #print(f"{candidate} received {vote_percentage:.1f}% of the vote.")
        ##print(f"{candidate}: {vote_percentage:.1f}% {votes:,}\n")

    # 5. The winner of the election based on popular vote

        if votes > winning_count and vote_percentage > winning_percentage:
            winning_count = votes
            winning_percentage = vote_percentage
            winning_candidate = candidate

     #print(winning_candidate_summary)

    winning_candidate_summary = (
        f"----------------------------\n"
        f"Winner: {winning_candidate}\n"
        f"Winning Vote: {winning_count:,}\n"
        f"Winning Percentage: {winning_percentage:.1f}\n"
    )
    print(winning_candidate_summary)
    txt_file.write(winning_candidate_summary)
    ```
