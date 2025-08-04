---
title: Track your Microsoft Secure Score history and meet goals
description: Gain insights into activity that has affected your Microsoft Secure Score. Discover trends and set goals.
ms.service: defender-xdr
ms.mktglfcycl: deploy
ms.localizationpriority: medium
f1.keywords:
  - NOCSH
ms.author: deniseb
author: denisebmsft
manager: dansimp
audience: ITPro
ms.collection: 
  - m365-security
  - tier2
ms.topic: concept-article
search.appverid: 
  - MOE150
  - MET150
ms.date: 04/28/2025
#customer intent: As an IT admin, I want to track my Microsoft Secure Score history and set goals so that I can improve my organization's security posture.
---

# Track your Microsoft Secure Score history and meet goals

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

[Microsoft Secure Score](microsoft-secure-score.md) is a measurement of an organization's security posture, with a higher number indicating more recommended actions taken. It can be found at https://security.microsoft.com/securescore in the [Microsoft Defender portal](microsoft-365-defender-portal.md).

## Gain insights into activity that has affected your score

View a graph of your organization's score over time in the **History** tab.

Below the graph is a list of all the actions taken in the selected time range and their attributes, such as resulting points and category. You can customize a date range and filter by category.

:::image type="content" source="/defender/media/secure-score/secure-score-history-activity.png" alt-text="An example of the page that describes the activity history in the Microsoft Defender portal" lightbox="/defender/media/secure-score/secure-score-history-activity.png":::

If you select the recommended action associated with an activity, the full recommended action flyout will appear.

To view all history for that specific recommended action, select the history link in the flyout.

:::image type="content" source="/defender/media/secure-score/secure-score-history-flyout.png" alt-text="The History pane regarding recommended action in the Microsoft Defender portal" lightbox="/defender/media/secure-score/secure-score-history-flyout.png":::

## Discover trends and set goals

In the **Metrics & trends** tab, there are several graphs and charts to give you more visibility into trends and set goals. You can set the date range for the whole page of visualizations. The visualizations include:

* **Your Secure Score zone** - Customized based on your organization's goals and definitions of good, okay, and bad score ranges.
* **Comparison trend** - How your organization's Secure Score compares to others' over time. This view can include lines representing the score average of organizations with similar seat count and a custom comparison view that you can set.
* **Score changes** - The number of points achieved, points regressed, and changes to your score in the specified date range.
* **Regression trend** - A timeline of points that have regressed because of configuration, user, or device changes.  
* **Risk acceptance trend** - Timeline of recommended actions marked as "risk accepted."

### Compare your score to organizations like yours

There are two places to see how your score compares to organizations that are similar to yours.

#### Comparison bar chart

The comparison bar chart is available on the **Overview** tab. Hover over the chart to view the score and score opportunity. 

:::image type="content" source="/defender/media/secure-score/secure-score-comparison-bar.png" alt-text="An example of the bar graph of similar organization's scores in the Microsoft Defender portal" lightbox="/defender/media/secure-score/secure-score-comparison-bar.png":::

The comparison data is anonymized so we don't know exactly which others tenants are in the mix.

![Bar graph of similar organization's scores.](/defender/media/secure-score/secure-score-comparison-screenshot.png)

#### Comparison trend

In the **Metrics & trends** tab, view how your organization's Secure Score compares to others' over time.

:::image type="content" source="/defender/media/secure-score/secure-score-comparison-trend.png" alt-text="An example of a line graph of similar organization's scores over time in the Microsoft Defender portal" lightbox="/defender/media/secure-score/secure-score-comparison-trend.png":::

## We want to hear from you

If you have any issues, let us know by posting in the [Defender XDR community](https://techcommunity.microsoft.com/category/microsoft-defender-xdr/discussions/microsoftthreatprotection). We're monitoring the community and will provide help.

## Related resources

- [Microsoft Secure Score overview](microsoft-secure-score.md)
- [Assess your security posture](microsoft-secure-score-improvement-actions.md)
- [What's coming](whats-new.md)
- [What's new](microsoft-secure-score-whats-new.md)
[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
