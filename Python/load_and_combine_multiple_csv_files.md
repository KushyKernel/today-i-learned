# Saving and combine multiple csv files 

```python

all_files = []
include = ['data']
path = r'C:\Users\Boluwatife.Kusimo\OneDrive - Navitas Pty Ltd\MI and Data Management\Data & MI\Datasets\hesa-data\graduate outcomes\graduate activities'
for root, dirs, files in os.walk(path):
    # dirs[:] = [d for d in dirs if d in include]
    for file in files:
        if (file.endswith(".csv")) & ("Table-6" in file):
            print(f"{file} --> to dataframe")
            all_files.append(os.path.join(root, file))
combined = pd.concat([pd.read_csv(f, skiprows=14, delimiter=',', header='infer') for f in all_files])
