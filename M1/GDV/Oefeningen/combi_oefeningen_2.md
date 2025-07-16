# Combi Oefeningen Les 2: Movement & Input

Kies 1 van de volgende oefeningen en voer die uit. Je mag er ook meer maken als je dat leuk vind en daar ook tijd voor over hebt.

## Inleveren werk

De oefeningen moeten jullie inleveren via een zogenaamde README.md file op Github.

Voor alle oefeningen geldt dat je een titel met de opdracht plaatst. Een korte omschrijving van wat je hebt gedaan, een gifje met daarin je werk goed in beeld gebracht en een link naar de code die bij de opdracht hoort.

[gebruik dit als template](../README.md#voorbeeld-readme-opdracht-format)

## Oefening 2.3A: Interactive Racing Game

### Doel

Combineer beweging, input en variabelen door een eenvoudig racing spel te maken.

### Wat ga je doen?

Bouw een auto die je kunt besturen met statistieken tracking en verschillende game modes.

### Stappen

#### Deel 1: Auto Movement System (Les 2.1 skills)

1. **Maak een nieuwe scene** genaamd "RacingGame"
2. **Bouw een auto:**

   - **Body:** Cube (geschaald naar auto vorm)
   - **Wheels:** 4 Cylinders als wielen
   - Organiseer in hierarchy als "Car" parent object

3. **Maak script** `CarController.cs`:

```csharp
public class CarController : MonoBehaviour
{
    [Header("Car Stats - Les 2.2")]
    public string driverName = "Speed Racer";
    public float maxSpeed = 15.0f;
    public float acceleration = 8.0f;
    public float turnSpeed = 100.0f;
    public bool hasNitro = true;
    public float nitroBoost = 25.0f;

    [Header("Current State - Les 2.2")]
    public float currentSpeed = 0.0f;
    public bool isAccelerating = false;
    public bool isBraking = false;
    public bool isUsingNitro = false;
    public int lapCount = 0;

    [Header("Game Stats - Les 2.2")]
    public float totalDistance = 0.0f;
    public float raceTime = 0.0f;
    public float topSpeed = 0.0f;

    void Start()
    {
        Debug.Log("RACING GAME STARTED");
        Debug.Log("Driver: " + driverName);
        Debug.Log("Controls: WASD = Drive, Space = Brake, Shift = Nitro");
        Debug.Log("Press I for car info, R to reset");
    }

    void Update()
    {
        HandleInput();      // Les 2.2: Input processing
        UpdateMovement();   // Les 2.1: Transform manipulation
        UpdateStats();      // Les 2.2: Variable management
        HandleDebugInput(); // Les 2.2: Additional input
    }

    void HandleInput() // Les 2.2: Input & Variables
    {
        // Reset states
        isAccelerating = false;
        isBraking = false;
        isUsingNitro = false;

        // Acceleration input
        if (Input.GetKey(KeyCode.W))
        {
            isAccelerating = true;
            currentSpeed += acceleration * Time.deltaTime;
        }

        // Deceleration
        if (Input.GetKey(KeyCode.S))
        {
            isBraking = true;
            currentSpeed -= acceleration * 1.5f * Time.deltaTime;
        }

        // Nitro boost
        if (Input.GetKey(KeyCode.LeftShift) && hasNitro && currentSpeed > 5.0f)
        {
            isUsingNitro = true;
            currentSpeed += nitroBoost * Time.deltaTime;
        }

        // Brake
        if (Input.GetKey(KeyCode.Space))
        {
            currentSpeed -= acceleration * 2.0f * Time.deltaTime;
        }

        // Natural slowdown
        if (!isAccelerating && !isBraking)
        {
            currentSpeed -= 2.0f * Time.deltaTime;
        }

        // Clamp speed
        float maxCurrentSpeed = isUsingNitro ? maxSpeed + 10.0f : maxSpeed;
        currentSpeed = Mathf.Clamp(currentSpeed, 0, maxCurrentSpeed);
    }

    void UpdateMovement() // Les 2.1: Transform Movement
    {
        // Forward movement
        transform.Translate(Vector3.forward * currentSpeed * Time.deltaTime);

        // Turning (only when moving)
        if (currentSpeed > 0.1f)
        {
            float turnInput = 0;
            if (Input.GetKey(KeyCode.A)) turnInput = -1;
            if (Input.GetKey(KeyCode.D)) turnInput = 1;

            float turnAmount = turnInput * turnSpeed * (currentSpeed / maxSpeed) * Time.deltaTime;
            transform.Rotate(0, turnAmount, 0);
        }
    }

    void UpdateStats() // Les 2.2: Variable Updates
    {
        // Update race time
        raceTime += Time.deltaTime;

        // Track distance
        totalDistance += currentSpeed * Time.deltaTime;

        // Track top speed
        if (currentSpeed > topSpeed)
        {
            topSpeed = currentSpeed;
        }
    }

    void HandleDebugInput() // Les 2.2: Additional Input
    {
        if (Input.GetKeyDown(KeyCode.I))
        {
            ShowCarInfo();
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            ResetCar();
        }
    }

    void ShowCarInfo()
    {
        Debug.Log("=== CAR INFO ===");
        Debug.Log("Driver: " + driverName);
        Debug.Log("Current Speed: " + currentSpeed.ToString("F1") + " / " + maxSpeed);
        Debug.Log("Race Time: " + raceTime.ToString("F1") + " seconds");
        Debug.Log("Distance: " + totalDistance.ToString("F1") + " units");
        Debug.Log("Top Speed: " + topSpeed.ToString("F1"));
        Debug.Log("Status: " + GetCarStatus());
        Debug.Log("===============");
    }

    string GetCarStatus()
    {
        if (isUsingNitro) return "NITRO BOOST!";
        if (isBraking) return "Braking";
        if (isAccelerating) return "Accelerating";
        if (currentSpeed < 0.1f) return "Stopped";
        return "Cruising";
    }

    void ResetCar()
    {
        transform.position = Vector3.zero;
        transform.rotation = Quaternion.identity;
        currentSpeed = 0;
        totalDistance = 0;
        raceTime = 0;
        topSpeed = 0;
        Debug.Log("Car reset!");
    }
}
```

#### Deel 2: Race Track Setup

4. **Bouw een simpele track:**
   - Gebruik **Plane** objecten als track secties
   - Voeg **Cube** barriers toe langs de zijkanten
   - Maak **Checkpoint** objecten (gekleurde Cylinders)

### Bonus Uitdagingen

- Voeg **fuel system** toe dat afneemt tijdens gebruik
- Maak **multiple car types** met verschillende stats
- Voeg **checkpoint** timing toe
- Implementeer **damage system** bij crashes

---

## Oefening 2.3B: Smart NPC Patrol System

### Doel

Maak intelligente NPCs die patrouilleren en reageren op de speler.

### Wat ga je doen?

Bouw NPCs met verschillende gedragsstaten en movement patterns.

### Stappen

#### Deel 1: NPC Movement AI (Les 2.1)

1. **Maak nieuwe scene** "NPCPatrol"
2. **Maak een NPC:** Capsule met ander materiaal dan speler

3. **Maak script** `NPCPatroller.cs`:

```csharp
public class NPCPatroller : MonoBehaviour
{
    [Header("NPC Identity - Les 2.2")]
    public string npcName = "Guard Bot";
    public string npcType = "Security";
    public int alertLevel = 0; // 0=Calm, 1=Suspicious, 2=Alert

    [Header("Movement Settings - Les 2.1")]
    public float patrolSpeed = 2.0f;
    public float chaseSpeed = 6.0f;
    public float rotationSpeed = 120.0f;

    [Header("Patrol Points - Les 2.1")]
    public Transform[] patrolPoints;
    public int currentPatrolIndex = 0;

    [Header("Detection - Les 2.2")]
    public float detectionRange = 5.0f;
    public bool playerDetected = false;
    public float suspicionTime = 0.0f;
    public string currentState = "Patrolling";

    [Header("Stats - Les 2.2")]
    public float totalDistanceWalked = 0.0f;
    public int playerDetectionCount = 0;
    public float timeOnDuty = 0.0f;

    private Transform player;
    private Vector3 lastPosition;

    void Start()
    {
        player = GameObject.FindWithTag("Player")?.transform;
        lastPosition = transform.position;

        if (patrolPoints.Length == 0)
        {
            Debug.LogWarning(npcName + " has no patrol points!");
        }

        Debug.Log("Robot " + npcName + " reporting for duty!");
        Debug.Log("Type: " + npcType);
    }

    void Update()
    {
        UpdateStats();          // Les 2.2: Variable tracking
        DetectPlayer();         // Les 2.2: Boolean logic
        UpdateBehavior();       // Les 2.1 + 2.2: Movement + States
        HandleDebugInput();     // Les 2.2: Input
    }

    void UpdateStats() // Les 2.2: Variables
    {
        timeOnDuty += Time.deltaTime;

        float distanceThisFrame = Vector3.Distance(transform.position, lastPosition);
        totalDistanceWalked += distanceThisFrame;
        lastPosition = transform.position;
    }

    void DetectPlayer() // Les 2.2: Boolean Logic
    {
        if (player == null) return;

        float distanceToPlayer = Vector3.Distance(transform.position, player.position);

        if (distanceToPlayer <= detectionRange)
        {
            if (!playerDetected)
            {
                playerDetected = true;
                playerDetectionCount++;
                suspicionTime = 0;
                Debug.Log(npcName + ": Player detected!");
            }

            suspicionTime += Time.deltaTime;

            // Alert level based on how long player is nearby
            if (suspicionTime > 3.0f)
                alertLevel = 2; // Alert
            else if (suspicionTime > 1.0f)
                alertLevel = 1; // Suspicious
            else
                alertLevel = 0; // Calm
        }
        else
        {
            if (playerDetected)
            {
                playerDetected = false;
                Debug.Log(npcName + ": Lost sight of player");
            }
            alertLevel = 0;
            suspicionTime = 0;
        }
    }

    void UpdateBehavior() // Les 2.1: Movement + Les 2.2: States
    {
        switch (alertLevel)
        {
            case 0: // Calm - Normal patrol
                currentState = "Patrolling";
                Patrol();
                break;

            case 1: // Suspicious - Slower movement
                currentState = "Suspicious";
                PatrolSlowly();
                break;

            case 2: // Alert - Chase player
                currentState = "Chasing";
                ChasePlayer();
                break;
        }
    }

    void Patrol() // Les 2.1: Transform Movement
    {
        if (patrolPoints.Length == 0) return;

        Transform targetPoint = patrolPoints[currentPatrolIndex];
        Vector3 direction = (targetPoint.position - transform.position).normalized;

        // Move towards patrol point
        transform.position += direction * patrolSpeed * Time.deltaTime;

        // Rotate towards target
        if (direction != Vector3.zero)
        {
            Quaternion targetRotation = Quaternion.LookRotation(direction);
            transform.rotation = Quaternion.Slerp(transform.rotation, targetRotation, rotationSpeed * Time.deltaTime);
        }

        // Check if reached patrol point
        if (Vector3.Distance(transform.position, targetPoint.position) < 0.5f)
        {
            currentPatrolIndex = (currentPatrolIndex + 1) % patrolPoints.Length;
        }
    }

    void PatrolSlowly() // Les 2.1: Modified Movement
    {
        if (patrolPoints.Length == 0) return;

        Transform targetPoint = patrolPoints[currentPatrolIndex];
        Vector3 direction = (targetPoint.position - transform.position).normalized;

        // Move slower when suspicious
        transform.position += direction * (patrolSpeed * 0.5f) * Time.deltaTime;

        // Look around occasionally
        if (suspicionTime % 2.0f < 0.1f)
        {
            transform.Rotate(0, 45, 0);
        }
    }

    void ChasePlayer() // Les 2.1: Movement towards target
    {
        if (player == null) return;

        Vector3 direction = (player.position - transform.position).normalized;

        // Move towards player
        transform.position += direction * chaseSpeed * Time.deltaTime;

        // Face player
        if (direction != Vector3.zero)
        {
            Quaternion targetRotation = Quaternion.LookRotation(direction);
            transform.rotation = Quaternion.Slerp(transform.rotation, targetRotation, rotationSpeed * 2 * Time.deltaTime);
        }
    }

    void HandleDebugInput() // Les 2.2: Input
    {
        if (Input.GetKeyDown(KeyCode.N))
        {
            ShowNPCInfo();
        }
    }

    void ShowNPCInfo()
    {
        Debug.Log("=== NPC INFO: " + npcName + " ===");
        Debug.Log("Type: " + npcType);
        Debug.Log("Current State: " + currentState);
        Debug.Log("Alert Level: " + alertLevel);
        Debug.Log("Time on Duty: " + timeOnDuty.ToString("F1") + " seconds");
        Debug.Log("Distance Walked: " + totalDistanceWalked.ToString("F1") + " units");
        Debug.Log("Player Detections: " + playerDetectionCount);
        Debug.Log("Player Nearby: " + playerDetected);
        Debug.Log("=============================");
    }
}
```

4. **Setup patrol points:**
   - Maak **Empty GameObjects** als patrol points
   - Plaats ze in een cirkel of pad
   - Sleep ze naar het **Patrol Points** array in de Inspector

#### Deel 2: Player Character

5. **Maak een Player** met eenvoudig movement script (gebruik eerdere oefening)

### Bonus Uitdagingen

- Voeg **multiple NPCs** toe met verschillende patrol routes
- Maak **communication** tussen NPCs
- Voeg **sound alerts** toe
- Implementeer **stealth mechanics**

---

## Oefening 2.3C: Dynamic Obstacle Course

### Doel

Bouw een parcours met bewegende obstakels en een timer systeem.

### Wat ga je doen?

Maak een parkour course waar speler doorheen moet navigeren terwijl obstakels bewegen.

### Stappen

#### Deel 1: Player + Parkour Movement

1. **Maak scene** "ObstacleCourse"
2. **Maak Player** met enhanced movement script

#### Deel 2: Moving Obstacles

3. **Maak script** `MovingObstacle.cs`:

```csharp
public class MovingObstacle : MonoBehaviour
{
    [Header("Obstacle Type - Les 2.2")]
    public string obstacleName = "Spinning Blade";
    public bool isActive = true;
    public bool isDeadly = true;

    [Header("Movement Pattern - Les 2.1")]
    public string movementType = "Rotating"; // Rotating, Linear, Pendulum
    public float speed = 90.0f;
    public Vector3 movementAxis = Vector3.up;
    public float distance = 5.0f;

    [Header("Timing - Les 2.2")]
    public float activationDelay = 0.0f;
    public float activeTime = 10.0f;
    public float restTime = 2.0f;

    [Header("Stats - Les 2.2")]
    public int playerHits = 0;
    public float timeActive = 0.0f;
    public bool playerNearby = false;

    private Vector3 startPosition;
    private float timer = 0.0f;
    private bool isMovingForward = true;

    void Start()
    {
        startPosition = transform.position;
        timer = activationDelay;

        Debug.Log("Obstacle '" + obstacleName + "' initialized");
        Debug.Log("Type: " + movementType + " | Deadly: " + isDeadly);
    }

    void Update()
    {
        timer += Time.deltaTime;

        if (timer >= activationDelay && isActive)
        {
            timeActive += Time.deltaTime;
            ExecuteMovement(); // Les 2.1: Transform manipulation
        }

        CheckNearbyPlayer(); // Les 2.2: Detection logic
    }

    void ExecuteMovement() // Les 2.1: Different movement patterns
    {
        switch (movementType)
        {
            case "Rotating":
                transform.Rotate(movementAxis * speed * Time.deltaTime);
                break;

            case "Linear":
                LinearMovement();
                break;

            case "Pendulum":
                PendulumMovement();
                break;

            case "Orbiting":
                OrbitMovement();
                break;
        }
    }

    void LinearMovement() // Les 2.1: Back and forth movement
    {
        Vector3 movement = movementAxis * speed * Time.deltaTime;

        if (!isMovingForward)
            movement = -movement;

        transform.position += movement;

        float distanceFromStart = Vector3.Distance(transform.position, startPosition);
        if (distanceFromStart >= distance)
        {
            isMovingForward = !isMovingForward;
        }
    }

    void PendulumMovement() // Les 2.1: Sine wave movement
    {
        float pendulumAngle = Mathf.Sin(Time.time * speed) * distance;
        Vector3 pendulumPosition = startPosition + movementAxis * pendulumAngle;
        transform.position = pendulumPosition;
    }

    void OrbitMovement() // Les 2.1: Circular movement
    {
        float angle = Time.time * speed;
        Vector3 orbitPosition = startPosition;
        orbitPosition.x += Mathf.Cos(angle) * distance;
        orbitPosition.z += Mathf.Sin(angle) * distance;
        transform.position = orbitPosition;
    }

    void CheckNearbyPlayer() // Les 2.2: Detection
    {
        GameObject player = GameObject.FindWithTag("Player");
        if (player != null)
        {
            float distanceToPlayer = Vector3.Distance(transform.position, player.position);
            playerNearby = distanceToPlayer < 3.0f;
        }
    }

    void OnTriggerEnter(Collider other) // Les 2.2: Collision response
    {
        if (other.CompareTag("Player"))
        {
            playerHits++;

            if (isDeadly)
            {
                Debug.Log(obstacleName + " hit player! (Hit #" + playerHits + ")");
                // Reset player or decrease health
                other.transform.position = Vector3.zero;
            }
            else
            {
                Debug.Log(obstacleName + " bumped player (Hit #" + playerHits + ")");
            }
        }
    }

    // Debug method to show obstacle info
    public void ShowObstacleInfo()
    {
        Debug.Log("=== OBSTACLE: " + obstacleName + " ===");
        Debug.Log("Movement: " + movementType);
        Debug.Log("Speed: " + speed);
        Debug.Log("Active: " + isActive);
        Debug.Log("Time Active: " + timeActive.ToString("F1") + "s");
        Debug.Log("Player Hits: " + playerHits);
        Debug.Log("Player Nearby: " + playerNearby);
        Debug.Log("==============================");
    }
}
```

#### Deel 3: Course Manager

4. **Maak script** `CourseManager.cs`:

```csharp
public class CourseManager : MonoBehaviour
{
    [Header("Course Info - Les 2.2")]
    public string courseName = "Deadly Gauntlet";
    public int difficulty = 3; // 1-5 scale
    public float courseTime = 0.0f;
    public bool courseCompleted = false;

    [Header("Player Stats - Les 2.2")]
    public int totalDeaths = 0;
    public float bestTime = 999.0f;
    public int checkpointsReached = 0;

    [Header("Course Objects")]
    public Transform startPoint;
    public Transform finishPoint;
    public MovingObstacle[] obstacles;

    private Transform player;
    private bool courseStarted = false;

    void Start()
    {
        player = GameObject.FindWithTag("Player")?.transform;

        if (player != null)
        {
            player.position = startPoint.position;
        }

        Debug.Log("Welcome to: " + courseName);
        Debug.Log("Difficulty: " + difficulty + "/5");
        Debug.Log("Press SPACE to start the course!");
        Debug.Log("Press O for obstacle info, C for course info");
    }

    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space) && !courseStarted)
        {
            StartCourse();
        }

        if (courseStarted && !courseCompleted)
        {
            courseTime += Time.deltaTime;
            CheckFinish();
        }

        if (Input.GetKeyDown(KeyCode.O))
        {
            ShowObstacleInfo();
        }

        if (Input.GetKeyDown(KeyCode.C))
        {
            ShowCourseInfo();
        }

        if (Input.GetKeyDown(KeyCode.R))
        {
            ResetCourse();
        }
    }

    void StartCourse()
    {
        courseStarted = true;
        courseTime = 0.0f;
        Debug.Log("Course started! Good luck!");
    }

    void CheckFinish()
    {
        if (player != null)
        {
            float distanceToFinish = Vector3.Distance(player.position, finishPoint.position);
            if (distanceToFinish < 2.0f)
            {
                CompleteCourse();
            }
        }
    }

    void CompleteCourse()
    {
        courseCompleted = true;

        if (courseTime < bestTime)
        {
            bestTime = courseTime;
            Debug.Log("NEW BEST TIME: " + bestTime.ToString("F2") + " seconds!");
        }

        Debug.Log("Course completed in " + courseTime.ToString("F2") + " seconds!");
        Debug.Log("Deaths: " + totalDeaths);
    }

    public void PlayerDied() // Called from other scripts
    {
        totalDeaths++;
        Debug.Log("Player died! (Death #" + totalDeaths + ")");

        if (player != null)
        {
            player.position = startPoint.position;
        }
    }

    void ShowObstacleInfo()
    {
        Debug.Log("=== OBSTACLE STATUS ===");
        for (int i = 0; i < obstacles.Length; i++)
        {
            if (obstacles[i] != null)
            {
                obstacles[i].ShowObstacleInfo();
            }
        }
    }

    void ShowCourseInfo()
    {
        Debug.Log("=== COURSE INFO ===");
        Debug.Log("Course: " + courseName);
        Debug.Log("Difficulty: " + difficulty + "/5");
        Debug.Log("Current Time: " + courseTime.ToString("F2") + "s");
        Debug.Log("Best Time: " + (bestTime < 999 ? bestTime.ToString("F2") + "s" : "None"));
        Debug.Log("Deaths: " + totalDeaths);
        Debug.Log("Completed: " + courseCompleted);
        Debug.Log("==================");
    }

    void ResetCourse()
    {
        courseStarted = false;
        courseCompleted = false;
        courseTime = 0.0f;

        if (player != null)
        {
            player.position = startPoint.position;
        }

        Debug.Log("Course reset!");
    }
}
```

### Bonus Uitdagingen

- Voeg **checkpoints** toe om voortgang op te slaan
- Maak **multiple difficulty levels**
- Implementeer **leaderboard system**
- Voeg **power-ups** toe die tijdelijk voordelen geven

---

## Tips voor Gecombineerde Oefeningen

### Architecture Tips

- **Deel logica op** tussen movement (Les 2.1) en state management (Les 2.2)
- Gebruik **public methods** om scripts met elkaar te laten communiceren
- Organiseer **related variables** met [Header] attributes

### Integration Best Practices

- Test **movement eerst**, voeg dan **variables en input** toe
- Gebruik **meaningful variable names** die duidelijk maken wat ze doen
- Voeg **debug output** toe om te zien hoe variables veranderen tijdens movement

### Performance Considerations

- Cache **transform references** in Start() voor bewegende objecten
- Gebruik **Time.deltaTime** voor alle time-based calculations
- Beperk **Debug.Log** output in Update() loops voor betere performance

---
