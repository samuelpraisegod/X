<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Prop Trading Platform</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body>
  <nav class="bg-gray-800 p-4">
    <div class="flex justify-center space-x-4 md:space-x-6">
      <button class="tab-button active px-4 py-2 rounded-full text-white font-semibold bg-white text-gray-800" data-tab="firms">Firms</button>
      <button class="tab-button px-4 py-2 rounded-full text-white hover:bg-gray-700" data-tab="challenges">Challenges</button>
      <button class="tab-button px-4 py-2 rounded-full text-white hover:bg-gray-700" data-tab="offers">Offers</button>
      <button class="tab-button px-4 py-2 rounded-full text-white hover:bg-gray-700" data-tab="reviews">Reviews</button>
    </div>
  </nav>

  <div id="firms" class="tab-content">
    <!-- Firms table as above -->
  </div>
  <div id="challenges" class="tab-content hidden">
    <!-- Challenges content as above -->
  </div>
  <div id="offers" class="tab-content hidden">
    <!-- Offers content as above -->
  </div>
  <div id="reviews" class="tab-content hidden">
    <!-- Reviews content as above -->
  </div>

  <script>
    // Tab switching logic as above
  </script>
</body>
</html>
