# Pagination ListView in Flutter

## Overview
This **Flutter** application demonstrates an **infinite scrolling list** using **Pagination ListView**. It dynamically loads data from an API as the user scrolls, ensuring efficient data fetching and smooth UI performance.

## Features
- ✅ **Infinite Scrolling** using `PagedListView` from `infinite_scroll_pagination`.
- ✅ **Efficient Data Fetching** from PunkAPI.
- ✅ **Pagination Support** to fetch data page by page.
- ✅ **Error Handling** to manage API failures.
- ✅ **Responsive UI** with image and text rendering.

## Tech Stack
- **Framework:** Flutter (Dart)
- **Networking:** HTTP package (`http`)
- **Pagination:** `infinite_scroll_pagination`
- **API:** PunkAPI (https://api.punkapi.com/v2/beers)

## Setup Instructions

### Prerequisites
- Install **Flutter** ([Installation Guide](https://flutter.dev/docs/get-started/install)).
- Ensure you have an active internet connection.

### Installation Steps
```sh
# Clone the repository
git clone <repository-url>

# Navigate to the project directory
cd <pagination_listview_directory>

# Get the dependencies
flutter pub get

# Run the application
flutter run
```

## Usage
1. Open the app.
2. Scroll down to load more data.
3. Data is fetched dynamically from the **PunkAPI**.
4. Images and names of items are displayed in a **ListTile** format.

## Dependencies
Add the following dependencies to your `pubspec.yaml`:
```yaml
dependencies:
  flutter:
    sdk: flutter
  http: latest_version
  infinite_scroll_pagination: latest_version
```

## Code Overview
### Fetching Data
```dart
void fetchData(int pageKey) async {
  try {
    var response = await http.get(Uri.parse("https://api.punkapi.com/v2/beers?page=$pageKey&per_page=10"));
    var data = dataModelFromJson(response.body);
    pagingController.appendPage(data, pageKey + 1);
  } catch (error) {
    pagingController.error = error;
  }
}
```

### Infinite Scrolling List
```dart
PagedListView<int, DataModel>(
  pagingController: pagingController,
  builderDelegate: PagedChildBuilderDelegate<DataModel>(
    itemBuilder: (context, model, index) => ListTile(
      title: Text(model.name),
      leading: Image.network(model.imageUrl),
    ),
  ),
)
```



