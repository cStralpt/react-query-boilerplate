# client state management in React Query
## NextJS


```
// app/layout.tsx
import type { Metadata } from "next";
import { Inter, Open_Sans } from "next/font/google";
import "./globals.css";
import ReactQueryProvider from "@/components/ReactQueryProvider";

const inter = Inter({ subsets: ["latin"] });
const openSans = Open_Sans({ preload: true, subsets: ["cyrillic"] });

export const metadata: Metadata = {
  title: "Ghifari Travel",
  description: "Ghifari melayani dengan hati dan hati-hati",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" className="light">
      <body className={openSans.className}>
        <ReactQueryProvider>
          {children}
        </ReactQueryProvider>
      </body>
    </html>
  );
}

```

```
"use client";
// app/page.tsx
import useRQGlobalState from "@/hooks/useRQGlobalState";

export default function Home() {
  const { data: user, setNewData: setNewUser } = useRQGlobalState({
    initialData: { userName: "my-name", email: "myeamil@example.com" },
    queryKey: ["user"],
  });
  return (
    <main className="">
      <p>{user?.userName}</p>
      <p>{user?.email}</p>
      <button
        onClick={() =>
          setNewUser({ userName: "new-name", email: "new-email@email.com" })
        }
      >
        Change Name
      </button>
    </main>
  );
}

```
