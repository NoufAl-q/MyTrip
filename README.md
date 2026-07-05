# MyTrip

An Android app for planning trips and packing checklists. Add a trip with a destination and date, build a packing checklist for it with priority levels, track how much you've packed, and share the plan with anyone.

Course project — **IT487, Mobile App Development**, Saudi Electronic University, College of Computing and Informatics.
Supervised by **Dr. Somayah Ali Hebah**.

## Features

- **Trips** — add, edit, and delete trips (destination + date), shown as a card list sorted by the closest upcoming date.
- **Packing checklist** — each trip has its own checklist of items, each with a priority (High / Normal / Low) and a checked/unchecked packed state.
- **Search** — live search across trips on the home screen and across items within a trip.
- **Dashboard** — total trips, total items, packed vs. remaining items, the next upcoming trip, and an overall completion rate.
- **Share** — share a trip's destination and full checklist as plain text via any installed app (`Intent.ACTION_SEND`).
- **Dark mode** — toggled from the home screen and persisted across launches.
- **Clear all data** — wipes all trips and items after a confirmation dialog.
- **About screen** — course, team, and supervisor information.

## Tech stack

| Piece | Technology | Why |
|---|---|---|
| Language | **Java** | Android app logic. |
| Persistence | **SQLite** (`SQLiteOpenHelper`) | Fully offline local storage — trips and packing lists are always available with no network dependency. |
| Lists | **RecyclerView + CardView** | Trip list and checklist rendering. |
| UI components | **Material Components** (`BottomNavigationView`, `FloatingActionButton`, `MaterialCardView`, `MaterialButton`) | Navigation, add actions, and card styling. |
| Sharing | **Android Intents** (`ACTION_SEND`) | Hands the trip/checklist text off to any app the user has installed, instead of a custom sharing implementation. |

## Data model

Two SQLite tables, managed by `DatabaseHelper`:

- **`trips`** — `id`, `destination`, `date`
- **`items`** — `id`, `trip_id` (FK to `trips`), `item_name`, `priority`, `is_checked`

Trips are queried both as "upcoming" (`date >= today`, ascending) for the home list and "recent"/past (`date < today`, descending) for the dashboard.

## Project structure

```
app/src/main/java/com/example/mytrip/
├── MainActivity.java            # Home: trip list, search, dark mode, add/delete trip
├── TripDetailActivity.java      # Checklist for one trip: add/edit/delete items, share
├── StatisticsActivity.java      # Dashboard: totals, completion rate, next trip
├── SupportActivity.java         # About: team, supervisor, course, contact
├── AddTripDialogFragment.java   # Add/edit trip dialog
├── AddItemDialogFragment.java   # Add/edit checklist item dialog
├── ContactDialogFragment.java   # Contact details dialog (from About screen)
├── DatabaseHelper.java          # SQLite schema + all CRUD/query/statistics functions
├── Trip.java / Item.java        # Data models
└── TripAdapter.java / ItemAdapter.java   # RecyclerView adapters
```

## Requirements

- Android Studio, minSdk 24, targetSdk 36.

## Running locally

```bash
./gradlew installDebug
```
or open the project in Android Studio and run the `app` configuration.

## Team

- Afnan Sanad Alharbi
- Nouf Ibrahim Al-Qurashi
- Rahaf Mohsen Alsulami
- Sara Mohammed Zain Abdulrahman
