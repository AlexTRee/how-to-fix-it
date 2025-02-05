## seaborn `distplot` is deprecated after Seaborn v0.11.0

The original `distplot` visualization<br>

![distplot](https://github.com/user-attachments/assets/1ed08b0a-3810-4106-93f3-49946c9c6488)

### The Issue
`displot`'s equivalent function `histplot`'s curve KDE starts only at the histogram bins' edges...

```diff
! sns.histplot(data[numerical_features[i]], kde=True, color="orange", stat="density",edgecolor="orange")
```
![histplot](https://github.com/user-attachments/assets/aa1e0336-5f4d-49a5-bf79-4dcf50c1acfc)

### FIX
- Adjust `cut` value.
- `cut` is a factor, multiplied by the smoothing bandwidth, that determines how far the evaluation grid extends past the extreme datapoints. When set to 0, truncate the curve at the data limits.

```diff
- # Plot histogram without KDE
+ sns.histplot(data[feature], color="orange", stat="density", edgecolor="orange", ax=axes[i])
- # Overlay KDE with extended range beyond first bin
+ sns.kdeplot(data[feature], color="blue", ax=axes[i], bw_adjust=0.5, cut=4, linewidth=1)
```
![hist+kde](https://github.com/user-attachments/assets/a1c925cf-d4de-4dee-b3f5-2e1881f3d906)


- Adjust `bw_adjust` value.
- `bw_adjust` is a factor, multiplicatively scales the value chosen using `bw_method`. Higher value means a smoother curve.
```diff
- # adjust bw_adjust to 1
+ sns.kdeplot(data[feature], color="blue", ax=axes[i], bw_adjust=1, cut=4, linewidth=1)
```
![hist+kde+bw](https://github.com/user-attachments/assets/e97e89bd-07e4-4b3e-9289-17d03b75c804)


