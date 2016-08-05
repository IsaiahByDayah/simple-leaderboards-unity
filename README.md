# simple-leaderboards-unity
Unity package for interfacing with a [simple-leaderboards](https://github.com/jordankid93/simple-leaderboards) backend

Version 0.0.1

## Dependencies:
- [JSONObject](https://github.com/mtschoen/JSONObject) ([Asset Store](https://www.assetstore.unity3d.com/en/#!/content/710))

## Usage

In the unity editor, attach the SimpleLeaderboardsManager script to the object that you want handling interacting with the leaderboards. In this example I create an empty object named "Test".

In the inspector, provide the SimpleLeaderboardsManager script with the base url for the server running an instance of [simple-leaderboards](https://github.com/jordankid93/simple-leaderboards).

![](https://github.com/jordankid93/simple-leaderboards-unity/blob/master/TestGameObject.png)

When you want to interact with the leaderboards, use the manager's `SubmitScore` and `FetchScoresForGame` functions.

```C#
public class Test : MonoBehaviour {

	private SimpleLeaderboardsManager lb;

	[SerializeField]
	private string gameTitle; // "Unity Test Game"

	void Start () {
		lb = GetComponent<SimpleLeaderboardsManager>();
	}
	
	void Update () {
		if (lb == null) return;

		// Submit
		if (Input.GetKeyDown(KeyCode.S))
		{
			lb.SubmitScore(gameTitle, 2, "SampleUser", ScoreSubmitted);
		}

		// Retrieve
		if (Input.GetKeyDown(KeyCode.R))
		{
			lb.FetchScoresForGame(gameTitle, HighScores);
		}
	}

	void HighScores(SimpleLeaderboardsScore[] scores)
	{
		Debug.Log("High Scores:");
		for (int i = 0; i < scores.Length; i++)
		{
			SimpleLeaderboardsScore s = scores[i];
			Debug.Log((i+1) + ") " + s.user + " - " + s.value);
		}
	}

	void ScoreSubmitted(SimpleLeaderboardsScore score)
	{
		Debug.Log("New Score:");
		Debug.Log(score.user + " - " + score.value);
	}
}
```
