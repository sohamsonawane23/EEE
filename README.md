```
flowchart TD
    %% Initial Node
    start([Start])

    %% Sequential Actions
    start --> Student_Presents_QR["Student Presents QR"]
    Student_Presents_QR --> Staff_Scans_QR["Staff Scans QR"]

    %% Decision 1: Token Valid?
    Staff_Scans_QR --> D1{Token Valid?}
    D1 -- No --> A_Error["Show Error"]
    A_Error --> end1([End])
    D1 -- Yes --> Fetch_Subscription["Fetch Subscription"]

    %% Decision 2: Within Slot Time?
    Fetch_Subscription --> D2{Within Slot Time?}
    D2 -- No --> A_Deny["Deny Redemption"]
    A_Deny --> end2([End])

    %% Fork/Join for Parallel Activities (simulate with split/merge)
    D2 -- Yes --> F1{{Fork}}
    F1 --> Deduct_Meal["Deduct Meal from Subscription"]
    F1 --> Log_Redemption["Log MealRedemption"]
    Deduct_Meal --> J1{{Join}}
    Log_Redemption --> J1

    %% Decision 3: RemainingMeals > 0?
    J1 --> D3{RemainingMeals > 0?}
    D3 -- No --> A_Expire["Set Subscription Expired"]
    A_Expire --> end3([End])
    D3 -- Yes --> Mark_Used["Mark Token Used"]

    %% Final Action and Final Node
    Mark_Used --> Show_Success["Show Success to Staff"]
    Show_Success --> end4([End])
```
```

### Option B: State diagram with forks/joins
If you prefer true UML semantics, use stateDiagram which supports <<fork>> and <<join>>.[3][6]
