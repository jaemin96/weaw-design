# Card Components

shadcn/ui와 Tailwind CSS 기반의 카드 컴포넌트 모음입니다.

## 컴포넌트 종류

### 1. Card (기본 shadcn 카드)

일반적인 카드 레이아웃을 위한 기본 컴포넌트

### 2. ThumbnailCard

썸네일과 제목을 표시하는 카드 컴포넌트

- 마우스 오버 시 스크롤바 자동 표시/숨김
- 썸네일 없을 때 아이콘 표시 옵션
- 선택 상태 표시

### 3. ThumbnailCardGrid

ThumbnailCard를 그리드로 배치하는 컴포넌트

## 필수 요구사항

- React
- Tailwind CSS
- `lucide-react` (아이콘용)
- `@/lib/utils`에 `cn` 유틸리티 함수

## 설치

### 1. lucide-react 설치 (아직 없다면)

```bash
npm install lucide-react
# or
pnpm add lucide-react
# or
yarn add lucide-react
```

### 2. 컴포넌트 파일 복사

`src/ui/card/` 폴더의 필요한 파일들을 프로젝트에 복사하세요.

**기본 카드만 필요한 경우:**

- `Card.tsx`

**썸네일 카드가 필요한 경우:**

- `Card.tsx` (기본 컴포넌트)
- `ThumbnailCard.tsx`
- `ThumbnailCardGrid.tsx` (옵션)

## 사용법

### 기본 Card 사용

```tsx
import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter } from "@/components/ui/card"

function Example() {
  return (
    <Card>
      <CardHeader>
        <CardTitle>Card Title</CardTitle>
        <CardDescription>Card Description</CardDescription>
      </CardHeader>
      <CardContent>
        <p>Card Content</p>
      </CardContent>
      <CardFooter>
        <p>Card Footer</p>
      </CardFooter>
    </Card>
  )
}
```

### ThumbnailCardGrid 사용

```tsx
import { ThumbnailCardGrid } from "@/components/ui/card"
import { useState } from "react"

function Example() {
  const [selectedId, setSelectedId] = useState<string | number>(1)

  const items = [
    { id: 1, thumbnail: "/images/thumb1.jpg", title: "Image 1" },
    { id: 2, thumbnail: "", title: "No Image" },
    { id: 3, thumbnail: "/images/thumb3.jpg", title: "Very long title that will scroll..." },
  ]

  return (
    <ThumbnailCardGrid
      items={items}
      selectedId={selectedId}
      onItemClick={setSelectedId}
      enableScroll={true}
      showNoImageIcon={false}
    />
  )
}
```

### 개별 ThumbnailCard 사용

```tsx
import { ThumbnailCard } from "@/components/ui/card"

function Example() {
  return (
    <ThumbnailCard
      thumbnail="/images/thumb.jpg"
      title="My Image"
      selected={true}
      onClick={() => console.log("clicked")}
      enableScroll={true}
      showNoImageIcon={false}
    />
  )
}
```

## Props

### Card

| Prop | Type | Description |
|------|------|-------------|
| `className` | `string` | 추가 CSS 클래스 |

### ThumbnailCard

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `thumbnail` | `string` | - | 썸네일 이미지 URL |
| `title` | `string` | required | 카드 제목 |
| `selected` | `boolean` | `false` | 선택 상태 |
| `onClick` | `() => void` | - | 클릭 핸들러 |
| `enableScroll` | `boolean` | `true` | 긴 텍스트 스크롤 활성화 |
| `showNoImageIcon` | `boolean` | `false` | 썸네일 없을 때 아이콘 표시 |
| `className` | `string` | - | 추가 CSS 클래스 |

### ThumbnailCardGrid

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `items` | `Array<{id, thumbnail?, title}>` | required | 표시할 아이템 배열 |
| `selectedId` | `string \| number` | - | 현재 선택된 아이템 ID |
| `onItemClick` | `(id) => void` | - | 아이템 클릭 핸들러 |
| `enableScroll` | `boolean` | `true` | 긴 텍스트 스크롤 활성화 |
| `showNoImageIcon` | `boolean` | `false` | 썸네일 없을 때 아이콘 표시 |
| `className` | `string` | - | 추가 CSS 클래스 |

## 주요 기능

### 1. 자동 스크롤바 표시/숨김 (ThumbnailCard)

- `enableScroll={true}`일 때, 마우스 오버 시 스크롤바 자동 표시
- 마우스를 떼면 자동으로 숨김
- 매우 얇고 투명한 스크롤바 디자인

```tsx
<ThumbnailCard
  title="Very long title..."
  enableScroll={true}  // 스크롤 활성화
/>
```

### 2. 썸네일 없을 때 처리

- 연한 회색 배경 (#fafafa)
- `showNoImageIcon={true}` 설정 시 흐린 이미지 아이콘 표시

```tsx
<ThumbnailCard
  thumbnail=""  // 빈 문자열 또는 undefined
  title="No Image"
  showNoImageIcon={true}  // 아이콘 표시
/>
```

### 3. 반응형 그리드

- 한 줄에 3개씩 고정 (`calc(33.333% - 0.5rem)`)
- flexbox 기반 자동 줄바꿈

### 4. 선택 상태 표시

- 선택된 카드는 primary 색상 테두리로 강조

```tsx
<ThumbnailCard
  title="Selected Card"
  selected={true}  // 선택 상태
/>
```

## 커스터마이징

### 색상 변경

ThumbnailCard.tsx에서 다음 클래스를 수정하세요:

- `border-primary`: 선택된 카드 테두리 색상
- `bg-[#fafafa]`: 썸네일 없을 때 배경색
- `text-black/[0.08]`: 아이콘 투명도

### 카드 크기 변경

- `w-[calc(33.333%-0.5rem)]`: 한 줄에 표시할 카드 개수 조정
  - 2개: `w-[calc(50%-0.5rem)]`
  - 4개: `w-[calc(25%-0.5rem)]`
- `max-h-[150px] min-h-[150px]`: 썸네일 높이
- `max-h-[60px]`: 텍스트 영역 최대 높이

### 스크롤바 스타일

Tailwind의 스크롤바 클래스로 커스터마이징:

```tsx
"[&::-webkit-scrollbar]:w-1"  // 스크롤바 너비
"group-hover:[&::-webkit-scrollbar-thumb]:bg-black/20"  // 스크롤바 색상
```

## 예제

### 다양한 옵션 조합

```tsx
import { ThumbnailCardGrid } from "@/components/ui/card"
import { useState } from "react"

export default function Example() {
  const [selectedId, setSelectedId] = useState<string | number>(1)

  const mockData = [
    { id: 1, thumbnail: "https://picsum.photos/200/150?random=1", title: "Short title" },
    { id: 2, thumbnail: "https://picsum.photos/200/150?random=2", title: "This is a very long title that will need scrolling to see the full content when it exceeds the maximum height" },
    { id: 3, thumbnail: "", title: "No thumbnail example" },
    { id: 4, thumbnail: "https://picsum.photos/200/150?random=4", title: "Another slide" },
    { id: 5, thumbnail: "", title: "Very_Long_File_Name_Without_Spaces_That_Should_Break_Properly_In_The_Card" },
    { id: 6, thumbnail: "https://picsum.photos/200/150?random=6", title: "Sample" },
  ]

  return (
    <div className="w-full max-w-4xl mx-auto p-4">
      <h1 className="text-2xl font-bold mb-4">Thumbnail Card Grid</h1>

      {/* 기본 사용 - 스크롤 ON, 아이콘 OFF */}
      <ThumbnailCardGrid
        items={mockData}
        selectedId={selectedId}
        onItemClick={setSelectedId}
        enableScroll={true}
        showNoImageIcon={false}
      />

      {/* 스크롤 OFF, 아이콘 ON */}
      <ThumbnailCardGrid
        items={mockData}
        selectedId={selectedId}
        onItemClick={setSelectedId}
        enableScroll={false}
        showNoImageIcon={true}
      />
    </div>
  )
}
```

## 파일 구조

``` bash
src/ui/card/
├── Card.tsx                    # 기본 shadcn 카드
├── ThumbnailCard.tsx          # 썸네일 카드
├── ThumbnailCardGrid.tsx      # 썸네일 그리드
├── index.ts                   # export 모음
└── README.md                  # 이 문서
```
