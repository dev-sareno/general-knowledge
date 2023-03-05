# Cross-origin resource sharing

## Example - Golang (Gin Gonic)
```go
func CORS() gin.HandlerFunc {
	return func(c *gin.Context) {
		reqOrigin := c.Request.Header["Origin"]
		if len(reqOrigin) > 0 {
			c.Header("Access-Control-Allow-Origin", reqOrigin[0])
			c.Header("Access-Control-Allow-Credentials", "true")
			c.Header("Access-Control-Allow-Headers", "Content-Type, Content-Length, Authorization, Accept, Origin, Access-Control-Allow-Credentials")
			c.Header("Access-Control-Allow-Methods", "POST, PATCH, OPTIONS, GET, PUT, DELETE")
		}

		if c.Request.Method == http.MethodOptions {
			c.Header("Cache-Control", "max-age=604800") // cache for 1 week
			c.AbortWithStatus(http.StatusNoContent)
			return
		}

		c.Next()
	}
}
```
