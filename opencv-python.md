## `opencv-python` installation got stuck <br><br>

```diff
- pip install opencv-python
```

<br>

`Python = 3.12.4`  `pip = 24.3.1`

<br>

```diff
! Collecting opencv-python
! Downloading opencv-python-4.11.0.86.tar.gz (95.2 MB)
!   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 95.2/95.2 MB 26.0 MB/s eta 0:00:00
! Installing build dependencies ... done
! Getting requirements to build wheel ... done
! Preparing metadata (pyproject.toml) ... done
! Requirement already satisfied: numpy>=1.21.2 in /Users/alexcui/anaconda3/envs/dev/lib/python3.12/site-packages (from opencv-python) (1.26.4)
! Building wheels for collected packages: opencv-python
! Building wheel for opencv-python (pyproject.toml) ...
```
### The Issue
By default, pip may attempt to build the wheel from source if it doesn't find a suitable prebuilt binary. For newer release of `opencv`, this could be the case.
<br>

### FIX
```diff
+ pip install opencv-python --only-binary :all:
```
<br>
This will skip building the wheel from source and use a precompiled binary instead.
