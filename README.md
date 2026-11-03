```javascript
function dailyLog221() {
  const logs = [
    { endpoint: "/api/users", status: 200 },
    { endpoint: "/api/login", status: 401 },
    { endpoint: "/api/orders", status: 500 },
    { endpoint: "/api/products", status: 200 },
    { endpoint: "/api/payment", status: 503 },
    { endpoint: "/api/profile", status: 404 },
    { endpoint: "/api/auth", status: 403 },
    { endpoint: "/api/reports", status: 500 },
  ];

  const errors = logs.filter(log => log.status >= 400);

  const categories = errors.reduce((result, log) => {
    const category = `${Math.floor(log.status / 100)}xx`;

    result[category] = (result[category] || 0) + 1;

    return result;
  }, {});

  const successCount = logs.length - errors.length;
  const successRate = (successCount / logs.length) * 100;

  console.log("=== API Error Monitoring Report ===");
  console.log(`Total Requests: ${logs.length}`);
  console.log(`Successful Requests: ${successCount}`);
  console.log(`Failed Requests: ${errors.length}`);
  console.log(`Success Rate: ${successRate.toFixed(2)}%`);

  console.log("\n=== Error Categories ===");

  Object.entries(categories).forEach(([code, count]) => {
    console.log(`${code}: ${count} errors`);
  });

  console.log("\n=== Failed Endpoints ===");

  errors.forEach(log => {
    console.log(`⚠️ ${log.endpoint} — HTTP ${log.status}`);
  });

  console.log("\n📊 Error analysis completed!");
}

dailyLog221();
```
