## NextJS API---> Transactions & Rollback

### heading...
![](https://imgur.com/ex0sviN.png)

```bash
import prisma from "@/lib/prisma";
import { NextRequest, NextResponse } from "next/server";


export async function GET(request: NextRequest) {
    try {

        
        const createUser = prisma.user.create({
            data: {
                name: "John Doe",
                email: "john.doe@example.com",
            }
        });

        const removePost = prisma.post.delete({
            where: {
                id: "be96c1cb-4d58-4f6a-9dd2-479e2d771271",
            }
        })

        const result = await prisma.$transaction([createUser, removePost]);
        

        return NextResponse.json(
            {status: "success", message: "Transaction completed successfully", data: result},
            {status: 200}
        )
    } catch (error) {
        return NextResponse.json(
            {status: "failed", message: "Internal server problem"},
            {status: 500}
        )
    }
}
```
---
