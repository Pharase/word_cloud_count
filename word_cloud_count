import pandas as pd
from pythainlp.tokenize import word_tokenize
from pythainlp.corpus.common import thai_stopwords
from collections import Counter
import matplotlib.pyplot as plt
from tqdm import tqdm

# Define the file path and read using pandas
file_path = r"C:\Pam\Proj\DB_report\processing\phone_code_keyword_1.xlsx"
df = pd.read_excel(file_path)

# Sampling information
n_percent = 50
sample_size = int(len(df) * n_percent / 100)
sampled_df = df.sample(n=sample_size, random_state=50)

# Get unique result codes
result_code = sampled_df['pamoareport_resultcodefromid'].unique()

# Iterate through each result code and process the text
for code in result_code:
    filtered_df = sampled_df[sampled_df['pamoareport_resultcodefromid'] == code]
    print(f"Result Code: {code}")
    
    # Concatenate all values in the 'pamoareport_info' column into a single string
    text = ' '.join(tqdm(filtered_df['pamoareport_info'].fillna('').astype(str).str.lower().tolist(), desc="Concatenating text"))
    
    # Tokenize the concatenated string into individual words
    tokens = word_tokenize(text, engine='newmm')
    
    # Count the frequency of each word
    word_counts = Counter(tokens)
    
    # Convert the Counter object to a DataFrame for better display
    word_counts_df = pd.DataFrame(word_counts.items(), columns=['Word', 'Count'])
    
    # Sort the DataFrame by count in descending order
    word_counts_df = word_counts_df.sort_values(by='Count', ascending=False)
    
    # Display the DataFrame
    print(word_counts_df.head(10))  # Display top 10 words for brevity
    
    # Plot the word counts
    #plt.figure(figsize=(10, 6))
    #plt.bar(word_counts_df['Word'][:10], word_counts_df['Count'][:10], color='skyblue')
    #plt.xlabel('Words')
    #plt.ylabel('Counts')
    #plt.title(f'Word Counts for Result Code: {code}')
    #plt.xticks(rotation=45)
    #plt.show()
