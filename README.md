# 🏆 CODE-A-THON

Welcome to the **Code-a-thon**! Test your data science and debugging skills by completing three challenging endpoints.

## 🎯 Challenge Overview

Your mission is to fix and complete three API endpoints:
1. **`POST /api/top-product`** - Modify to return TOP 5 products (Easy)
2. **`GET /api/categories`** - Complete the implementation (Medium) 
3. **`GET /api/demographics`** - Debug multiple bugs (Hard)

## 📋 Dataset Information

The `sales_data.csv` contains 250 e-commerce transactions with:
- **Products**: 20+ unique items across 6 categories
- **Categories**: Electronics, Clothing, Books, Home, Sports, Beauty
- **Time Range**: 6 months of sales data (Jan-Aug 2024)
- **Customers**: Ages 18-65 for demographic analysis
- **Test Data**: "Test Widget" entries for auto-evaluation

### Key Columns
- `transaction_id`: Unique transaction identifier
- `product_name`: Product names (includes "Test Widget" for testing)
- `category`: Product categories for analysis
- `price`: Product prices ($5-$2000 range)
- `quantity`: Purchase quantities (1-5 items)
- `customer_age`: Customer ages (18-65)
- `purchase_date`: Transaction dates
- `customer_rating`: Product ratings (1-5 stars, some missing)
- `revenue`: Calculated revenue (price × quantity)

## 🚀 Quick Start

### 1. Fork the Repository

1. Go to the [GitHub repository](https://github.com/alumnx-ai-labs/codeathon).
2. Click the **"Fork"** button in the top right corner.
3. Choose your GitHub account as the destination.

### 2. Clone Your Fork

Replace `<your-username>` with your GitHub username:

```bash
git clone https://github.com/<your-username>/codeathon.git
cd codeathon
```

### 3. Create Virtual Environment

#### For Linux/Mac:
```bash
python3 -m venv venv
source venv/bin/activate
```

#### For Windows:
```bash
python -m venv venv
# Command Prompt:
venv\Scripts\activate
# PowerShell:
venv\Scripts\Activate.ps1
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Run the FastAPI Service

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
# or you can also use
# python main.py
```

The API will be available at:
- **Main URL**: http://localhost:8000
- **Health Check**: http://localhost:8000/health

## 🧪 Testing the API

### Health Check
```bash
curl http://localhost:8000/health
```

### Data Info (Debug Helper)
```bash
curl http://localhost:8000/api/data-info
```

## 📋 Challenge Details & API Endpoints

### 🎯 Challenge 1: `/api/top-product` (Easy - 20 points)

**Task**: Modify to return TOP 5 products instead of TOP 3

#### Request:
```bash
curl -X POST "http://localhost:8000/api/top-product" \
     -H "Content-Type: application/json" \
     -d '{"month": "2024-03"}'
```

#### Expected Response:
```json
{
  "month": "2024-03",
  "top_products": [
    {
      "product_name": "Laptop Pro",
      "revenue": 1500.00,
      "category": "Electronics"
    },
    {
      "product_name": "Smartphone X",
      "revenue": 1200.00,
      "category": "Electronics"
    }
    // ... 3 more products (total 5)
  ],
  "total_revenue": 15000.00
}
```

**What to do**: Find and change the line that limits results to 3 products.

---

### 🎯 Challenge 2: `/api/categories` (Medium - 40 points)

**Task**: Complete the entire implementation from scratch

#### Request:
```bash
curl http://localhost:8000/api/categories
```

#### Expected Response:
```json
{
  "categories": [
    {
      "category": "Electronics",
      "total_revenue": 15000.50,
      "avg_revenue_per_transaction": 125.25,
      "transaction_count": 120,
      "avg_rating": 4.2,
      "total_units_sold": 350,
      "revenue_percentage": 35.5
    }
    // ... more categories
  ],
  "total_categories": 6
}
```

**What to do**: 
- Implement groupby operations on sales data
- Calculate all required metrics
- Handle null values appropriately
- Calculate revenue percentages

---

### 🎯 Challenge 3: `/api/demographics` (Hard - 40 points)

**Task**: Debug and fix multiple bugs in the code

#### Request:
```bash
curl http://localhost:8000/api/demographics
```

#### Expected Response:
```json
{
  "age_groups": [
    {
      "age_range": "18-25",
      "customer_count": 150,
      "avg_spending": 85.50,
      "total_revenue": 12825.00,
      "avg_rating": 4.1,
      "transaction_count": 150,
      "revenue_percentage": 25.5
    }
    // ... more age groups
  ],
  "summary": {
    "total_customers": 600,
    "highest_spending_group": "26-35",
    "largest_group": "26-35", 
    "highest_rated_group": "46-55"
  }
}
```

**What to do**:
- Fix syntax errors that cause crashes
- Debug column mapping issues
- Fix variable naming problems
- Correct calculation logic
- Handle missing data appropriately

**Hints for debugging**:
- Check error messages carefully
- Verify column names match the dataset
- Ensure aggregation columns align with assignments
- Test each section independently


## 🚀 Pushing Your Code to GitHub

After making changes, you need to push your code to your forked repository on GitHub.

### First Time Push

```bash
git add .
git commit -m "Your commit message"
git push -u origin main
```

### Subsequent Pushes

```bash
git add .
git commit -m "Describe your changes"
git push
```

## 🚀 Deploying to Render

### 🔹 Step 1: Access Render Dashboard

**Go to** [https://dashboard.render.com](https://dashboard.render.com) and **log in** with your GitHub account.

---

### 🔹 Step 2: Start a New Web Service

* **First-time users:** After logging in, you'll land directly on the *"Create a New Service"* page.
  → Click **"Web Service"**.

* **Returning users:** On the Render dashboard, go to the top-right and click **`+ Add new`**, then choose **"Web Service"**.

---

### 🔹 Step 3: Connect Your GitHub Repository

At the top of the "Configure and Deploy Your New Web Service" page:

* Click the **"Credentials"** dropdown next to the search bar.
* Under **Connected Deployment Credentials**, click your **GitHub username**.
* Click **"Configure GitHub"**.

  * Under *Repository Access*, choose **"Only select repositories"**.
  * From the dropdown, **select `codeathon`** and click **Save**.

Now you'll see `codeathon` appear in the repository dropdown.
→ Select it.

---

### 🔹 Step 4: Configure the Service

* In the **Name** field, replace the default with a custom name that includes **your KahootQuiz username** (e.g., `codeathon-yourname`).
* Scroll down to **"Instance Type"** and select **Free**.
* Just above that, in **"Start Command"**, paste the following:

  ```
  uvicorn main:app --host 0.0.0.0 --port $PORT
  ```

---

### 🔹 Step 5: Deploy

* Scroll to the bottom and click **"Create Web Service"** or **"Deploy Web Service"**.

Render will now build and deploy your app. This may take a minute or two. Once it's live, you'll get a URL you can visit to see your app in action.

---

### 🔄 Redeploying & Auto-Deploy on Commit

- **Auto-Deploy:**  
  Render will automatically redeploy your service every time you push changes to your connected GitHub repository.  
  1. Make your code changes locally.
  2. Commit and push:
     ```sh
     git add .
     git commit -m "Describe your changes"
     git push
     ```
  3. Render will detect the new commit and redeploy automatically.

- **Manual Redeploy:**  
  If you want to force a redeploy without pushing new commits:
  1. Go to your service dashboard on [render.com](https://render.com/).
  2. Click your service (e.g., `codeathon-yourname`).
  3. Click the **Manual Deploy** button and select **Deploy latest commit**.

### Alternative: Using render.yaml (Advanced)

> **Note:**  
> A `render.yaml` file is already included in this repository.  
> You do **not** need to create it yourself.

If you want to use Infrastructure as Code, the provided `render.yaml` file will be used automatically by Render:

```yaml
services:
  - type: web
    name: ecommerce-analytics-api
    env: python
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn solution_script:app --host 0.0.0.0 --port $PORT
    envVars:
      - key: PYTHON_VERSION
        value: 3.9.16
```

**Benefits of render.yaml**:
- ✅ Automatic configuration deployment
- ✅ Version control for infrastructure settings
- ✅ Consistent deployments across environments
- ✅ Easy to replicate and share configurations

**When to use render.yaml**:
- You want infrastructure as code
- You need consistent deployment settings
- You're deploying multiple services
- You want to version control your deployment configuration

## 📚 Documentation References

### FastAPI Resources
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [FastAPI Tutorial](https://fastapi.tiangolo.com/tutorial/)
- [Pydantic Models](https://pydantic-docs.helpmanual.io/)

### Pandas Resources  
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [GroupBy Operations](https://pandas.pydata.org/docs/user_guide/groupby.html)
- [Data Aggregation](https://pandas.pydata.org/docs/user_guide/groupby.html#aggregation)

### Python Debugging
- [Python Debugging Guide](https://realpython.com/python-debugging-pdb/)
- [Common Python Errors](https://realpython.com/python-traceback/)

### Deployment
- [Render Deployment Guide](https://render.com/docs)
- [Python Apps on Render](https://render.com/docs/deploy-fastapi)

## 🏆 Scoring Criteria

- **Challenge 1**: 20 points - Simple modification
- **Challenge 2**: 40 points - Complete implementation  
- **Challenge 3**: 40 points - Multiple bug fixes
- **Bonus Points**: Code quality, error handling, documentation

## 🛠️ Development Tips

1. **Use the `/api/data-info` endpoint** to understand the dataset structure
2. **Test incrementally** - fix one bug at a time
3. **Read error messages carefully** - they contain valuable debugging info
4. **Use curl commands or Postman** for API testing
5. **Check column names** in the actual CSV file if needed

## 🆘 Getting Help

- Check the API endpoints using curl commands or Postman
- Use the `/health` endpoint to verify the service is running
- Use the `/api/data-info` endpoint to inspect the dataset
- Review error logs in the terminal for debugging clues

## 📝 Submission

1. Complete all three challenges
2. Test all endpoints locally
3. Deploy to Render 
4. **Submit your Render deployment URL** (e.g., `https://your-app-name.onrender.com`)

**Note**: Make sure your deployed API is working and all endpoints are accessible before submission.

Good luck, and may the best data scientist win! 🚀

---

**Happy Coding!** 🎉s