Import https://assetstore.unity.com/packages/tools/integration/daily-rewards-free-110798  Daily Rewards - Free


and import this package

make a script name DailyRewardsManager

and paste this code

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using NiobiumStudios;
using System;

public class DailyRewardsManager : MonoBehaviour
{
    public PlayerManager playerManager;
    private void Start()
    {
        playerManager = FindAnyObjectByType<PlayerManager>();
    }
    private void OnEnable()
    {
        DailyRewards.instance.onClaimPrize += OnClaimPrizeDailyRewards;
    }

    private void OnDisable()
    {
        DailyRewards.instance.onClaimPrize -= OnClaimPrizeDailyRewards;
    }

    private void OnClaimPrizeDailyRewards(int day)
    {
        Reward reward = DailyRewards.instance.GetReward(day);

        print(reward.unit);
        print(reward.reward);


        // replace this by your own logic

        if (playerManager != null)
        {
            if (reward.unit == "Coins")
            {
                playerManager.AddScore(reward.reward);
            }
        }
        else
        {
            print("Unable to find PlayerManager");
        }

    }
}
