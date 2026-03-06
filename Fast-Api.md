# FastAPI

## Default sequence:
```lua
cliente
   ↓
TCP
   ↓
uvicorn
   ↓
ASGI call
   ↓
Starlette router
   ↓
FastAPI dependency resolver
   ↓
Pydantic validation
   ↓
sua função
   ↓
serialização JSON
   ↓
response
   ↓
uvicorn
   ↓
cliente
```

