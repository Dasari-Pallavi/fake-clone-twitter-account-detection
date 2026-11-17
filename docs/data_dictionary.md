# Data Dictionary

## 1. Raw Dataset Columns (`data/raw/twitter_bot_data.csv`)

| Column Name | Data Type | Business Description |
| :--- | :--- | :--- |
| `User ID` | Integer | Unique identifier assigned to each Twitter account. |
| `Username` | String | Public handle/display identifier of the account. |
| `Tweet` | String | Sample post text associated with the account. |
| `Retweet Count` | Integer | Number of retweets recorded on the account's post. |
| `Mention Count` | Integer | Number of user mentions included in the post. |
| `Follower Count` | Integer | Total number of followers following the account. |
| `Verified` | Boolean | Indicates whether the account holds verified badge status (`True`/`False`). |
| `Bot Label` | Integer | Target classification label (`1` = Fake/Bot account, `0` = Genuine human account). |
| `Location` | String | Self-reported geographic location on the user profile. |
| `Created At` | DateTime | Timestamp when the account or post record was created. |
| `Hashtags` | String | Space-separated hashtags used within the tweet content. |

## 2. Engineered Behavioral KPIs & Outputs (`data/processed/cleaned_data.csv` & `outputs/predictions.csv`)

| Feature / Output Name | Formula / Logic | Analytical Purpose |
| :--- | :--- | :--- |
| `tweet_length` | Character count of `tweet` | Detects templated or abnormally short/long automated posts. |
| `hashtag_count` | Count of tokens in `hashtags` | Measures hashtag stuffing typical of spam bots. |
| `has_location` | `1` if `location != "Unknown"`, else `0` | Tracks profile completeness (bots often leave profiles blank). |
| `account_age_days` | Days elapsed since `created_at` | Identifies newly created throwaway accounts. |
| `engagement` | `retweet_count + mention_count` | Combined interaction volume per account. |
| `username_len` | Character length of `username` | Captures auto-generated handle lengths. |
| `username_digits` | Count of numeric digits in `username` | Flags default/auto-generated handles (e.g., `user839201`). |
| `nearest_dist` | Euclidean distance to closest neighbor | Measures behavioral similarity across standardized features. |
| `fake_probability` | Random Forest predicted probability (`0–1`) | Likelihood score that an account is automated/fake. |
| `risk_tier` | `Low` (`<=0.5`), `Medium` (`0.5–0.8`), `High` (`>0.8`) | Routes accounts into prioritized Trust & Safety review queues. |
