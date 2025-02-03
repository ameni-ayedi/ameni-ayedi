import matplotlib.pyplot as plt
import requests
import json

# Replace with your GitHub username
GITHUB_USERNAME = "yourusername"

# Fetch GitHub statistics
url = f"https://api.github.com/users/{GITHUB_USERNAME}/repos"
response = requests.get(url)
repos = json.loads(response.text)

# Extract data (repo names and stars)
repo_names = [repo["name"] for repo in repos[:5]]  # Top 5 repos
repo_stars = [repo["stargazers_count"] for repo in repos[:5]]

# Create a bar plot for stars per repo
plt.figure(figsize=(8, 4))
plt.barh(repo_names, repo_stars, color="skyblue")
plt.xlabel("Stars")
plt.ylabel("Repositories")
plt.title(f"GitHub Stars for {GITHUB_USERNAME}")
plt.gca().invert_yaxis()
plt.savefig("github_stats.png")  # Save the plot as an image

# Create a contribution pie chart (example data)
plt.figure(figsize=(4, 4))
contributions = [70, 20, 10]  # Example: Code, Issues, PRs
labels = ["Code", "Issues", "PRs"]
plt.pie(contributions, labels=labels, autopct="%1.1f%%", colors=["blue", "green", "red"])
plt.title("GitHub Contribution Breakdown")
plt.savefig("github_contributions.png")  # Save the plot as an image
plt.show()
