import matplotlib.pyplot as plt
import requests
import json

# Your GitHub username
GITHUB_USERNAME = "ameni-ayedi"

# Fetch GitHub repository statistics
url = f"https://api.github.com/users/{GITHUB_USERNAME}/repos"
response = requests.get(url)
repos = json.loads(response.text)

# Extract repo names and stars (Top 5 repos with most stars)
sorted_repos = sorted(repos, key=lambda x: x["stargazers_count"], reverse=True)[:5]
repo_names = [repo["name"] for repo in sorted_repos]
repo_stars = [repo["stargazers_count"] for repo in sorted_repos]

# Create a bar plot for stars per repo
plt.figure(figsize=(8, 4))
plt.barh(repo_names, repo_stars, color="skyblue")
plt.xlabel("Stars ⭐")
plt.ylabel("Repositories 📂")
plt.title(f"GitHub Stars for ameni-ayedi")
plt.gca().invert_yaxis()
plt.savefig("github_stats.png")  # Save the plot as an image

# Fetch user contribution stats
url_contribs = f"https://api.github.com/users/ameni-ayedi"
response_contribs = requests.get(url_contribs)
user_data = json.loads(response_contribs.text)
total_contributions = user_data.get("public_repos", 0) + user_data.get("followers", 0) + user_data.get("following", 0)

# Create a GitHub contribution pie chart (example proportions)
contributions = [user_data.get("public_repos", 0), user_data.get("followers", 0), user_data.get("following", 0)]
labels = ["Repositories", "Followers", "Following"]
plt.figure(figsize=(4, 4))
plt.pie(contributions, labels=labels, autopct="%1.1f%%", colors=["blue", "green", "red"])
plt.title(f"GitHub Contribution Breakdown for ameni-ayedi")
plt.savefig("github_contributions.png")  # Save the plot as an image
plt.show()
