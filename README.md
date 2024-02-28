# Importing necessary libraries
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
# Loading the dataset
data = pd.read_csv('las_vegas_airbnb_data.csv')
print(data.columns)
def plot_heatmap(data, columns):
    """
    Plot a heatmap (correlation matrix) for the specified columns in the given dataset.

    Parameters:
    - data (DataFrame): The dataset.
    - columns (list): List of columns for which to plot the heatmap.
    """
    # Select only the specified columns
    selected_data = data[columns]
    
    # Filter out non-numeric columns
    numeric_data = selected_data.select_dtypes(include=['float64', 'int64'])

    # Calculate correlation matrix
    correlation_matrix = numeric_data.corr()

    # Plot heatmap
    plt.figure(figsize=(10, 8))
    sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
    plt.title('Correlation Matrix')
    plt.show()
def plot_scatter(data, x_column, y_column):
    """
    Plot a scatter plot for the specified columns in the given dataset.

    Parameters:
    - data (DataFrame): The dataset.
    - x_column (str): The column for the x-axis.
    - y_column (str): The column for the y-axis.
    """
    plt.figure(figsize=(8, 6))
    plt.scatter(data[x_column], data[y_column], color='green')
    plt.title(f'{x_column} vs {y_column}')
    plt.xlabel(x_column)
    plt.ylabel(y_column)
    plt.grid(True)
    plt.show()

def plot_pie(data, column):
    """
    Plot a pie chart for the specified column in the given dataset.

    Parameters:
    - data (DataFrame): The dataset.
    - column (str): The column for which to plot the pie chart.
    """
    plt.figure(figsize=(8,8))
    data[column].value_counts().plot(kind='pie', autopct='%1.1f%%')
    plt.title(f'Distribution of {column}')
    plt.ylabel('')
    plt.show()
    plot_heatmap(data, ['roomType', 'numberOfGuests', 'firstReviewRating','stars'])
    plot_scatter(data, 'numberOfGuests', 'firstReviewRating')
    plot_pie(data.head(20), 'roomType')
    # Descriptive statistics of the dataset
print(data.describe())
# Correlation matrix for numeric columns
numeric_data = data.select_dtypes(include='number')
correlation_matrix = numeric_data.corr()
print(correlation_matrix)
