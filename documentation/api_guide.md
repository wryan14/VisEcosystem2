# Library Visualization API Documentation

## Data Management Endpoints

### Upload Dataset
- **Endpoint**: `/api/data/upload`
- **Method**: POST
- **Description**: Upload a new dataset (CSV or Excel)
- **Parameters**: Form data with 'file' field
- **Returns**: Dataset ID and name
- **Example Response**:
```json
{
    "message": "File uploaded successfully",
    "dataset_id": 123,
    "name": "circulation_2024.csv"
}
```

### Preview Dataset
- **Endpoint**: `/api/data/preview/<dataset_id>`
- **Method**: GET
- **Description**: Get a preview of dataset contents (samples first 1000 rows for large datasets)
- **Returns**: Data preview, columns, and row count
- **Example Response**:
```json
{
    "data": [...],
    "columns": ["date", "checkouts", "renewals"],
    "row_count": 1000
}
```

### Delete Dataset
- **Endpoint**: `/api/dataset/<dataset_id>/delete`
- **Method**: DELETE
- **Description**: Delete a dataset and its associated file
- **Returns**: Success message
- **Example Response**:
```json
{
    "success": true,
    "message": "Dataset deleted successfully"
}
```

## Visualization Endpoints

### Save Visualization
- **Endpoint**: `/api/viz/save`
- **Method**: POST
- **Description**: Save a new visualization
- **Required Fields**: name, chart_type, config
- **Example Request Body**:
```json
{
    "name": "Monthly Circulation",
    "chart_type": "line",
    "config": {...},
    "category": "Circulation",
    "description": "Monthly circulation trends"
}
```

### Update Visualization
- **Endpoint**: `/api/viz/<viz_id>/update`
- **Method**: POST
- **Description**: Update an existing visualization
- **Returns**: Success message
- **Example Request Body**:
```json
{
    "name": "Updated Name",
    "chart_type": "bar",
    "config": {...}
}
```

### Delete Visualization
- **Endpoint**: `/api/viz/<viz_id>/delete`
- **Method**: DELETE
- **Description**: Delete a visualization
- **Returns**: Success message

### Get Visualization Config
- **Endpoint**: `/api/config/<viz_id>`
- **Method**: GET
- **Description**: Get visualization configuration with optional data clearing
- **Query Parameters**: 
  - `clear_data=true` (optional): Returns config with empty data arrays
- **Returns**: Visualization config and metadata
- **Example Response**:
```json
{
    "id": 123,
    "name": "Monthly Circulation",
    "chart_type": "line",
    "config": {
        "data": [{
            "type": "scatter",
            "x": [],
            "y": []
        }],
        "layout": {...}
    },
    "category": "Circulation",
    "description": "Monthly circulation trends"
}
```

### Recent Visualizations
- **Endpoint**: `/api/recent`
- **Method**: GET
- **Description**: Get list of recent visualizations
- **Returns**: List of recent visualizations with metadata
- **Example Response**:
```json
{
    "visualizations": [
        {
            "id": 123,
            "name": "Monthly Circulation",
            "chart_type": "line",
            "category": "Circulation",
            "created_at": "2024-01-08 14:30:00",
            "updated_at": "2024-01-08 15:45:00"
        }
    ]
}
```

## Template Endpoints

### Get Templates
- **Endpoint**: `/api/templates`
- **Method**: GET
- **Description**: Get available templates, optionally filtered by category
- **Query Parameters**: 
  - `category` (optional): Filter templates by category
- **Returns**: List of templates
- **Example Response**:
```json
{
    "templates": [
        {
            "id": 1,
            "name": "Circulation Trends",
            "category": "Circulation",
            "chart_type": "line",
            "config": {...}
        }
    ]
}
```

## Error Handling
All endpoints return appropriate HTTP status codes:
- 200: Success
- 400: Bad Request (missing or invalid parameters)
- 404: Not Found (resource doesn't exist)
- 500: Internal Server Error

Error responses include a descriptive message:
```json
{
    "error": "Error description here"
}
```