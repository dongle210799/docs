# Quy ước viết code <!-- omit in toc -->

## Mục lục <!-- omit in toc -->

- [Giới thiệu](#giới-thiệu)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
  - [Mô tả thư mục](#mô-tả-thư-mục)
    - [api](#api)
    - [assets](#assets)
    - [components](#components)
    - [constants](#constants)
    - [css](#css)
    - [hooks](#hooks)
    - [lib](#lib)
    - [pages](#pages)
    - [router](#router)
    - [stores](#stores)
    - [types](#types)
- [Thông số file](#thông-số-file)
- [Định dạng](#định-dạng)
- [TypeScript](#typescript)
  - [Biến](#biến)
  - [Hàm](#hàm)
  - [Tên biến・Tên hàm](#tên-biếntên-hàm)
    - [Quy tắc cơ bản](#quy-tắc-cơ-bản)
    - [Event Handler](#event-handler)
  - [Comment](#comment)
  - [Kiểu dữ liệu](#kiểu-dữ-liệu)
  - [Class](#class)
  - [Interface](#interface)
  - [Type](#type)
  - [Interface vs Type](#interface-vs-type)
  - [Enum](#enum)
  - [null vs undefined](#null-vs-undefined)
  - [Mảng](#mảng)
    - [Định nghĩa kiểu](#định-nghĩa-kiểu)
    - [Truy cập phần tử mảng](#truy-cập-phần-tử-mảng)
  - [Object](#object)
  - [Rẽ nhánh điều kiện](#rẽ-nhánh-điều-kiện)
  - [Console log](#console-log)
  - [Tên file](#tên-file)
  - [Import](#import)
  - [Export](#export)
- [React](#react)
  - [Component](#component)
  - [Khai báo biến](#khai-báo-biến)
  - [Event Handler](#event-handler-1)
  - [Import/Export Component](#importexport-component)
    - [Import](#import-1)
    - [Export](#export-1)
    - [JSX Tag](#jsx-tag)
    - [Fragment](#fragment)
    - [Hook](#hook)
  - [Định nghĩa kiểu liên quan đến React](#định-nghĩa-kiểu-liên-quan-đến-react)
    - [Import kiểu](#import-kiểu)
    - [Định nghĩa kiểu Component](#định-nghĩa-kiểu-component)
    - [Định nghĩa kiểu props](#định-nghĩa-kiểu-props)
  - [Cách nhận props](#cách-nhận-props)
- [Phương hướng xử lý lỗi](#phương-hướng-xử-lý-lỗi)
  - [Lỗi API (đã xác thực)](#lỗi-api-đã-xác-thực)
  - [Lỗi API (chưa xác thực)](#lỗi-api-chưa-xác-thực)
  - [Lỗi JavaScript (xử lý ngoại lệ)](#lỗi-javascript-xử-lý-ngoại-lệ)
- [Styling](#styling)
- [Bảo mật (thông tin bí mật)](#bảo-mật-thông-tin-bí-mật)
- [Hỗ trợ đa ngôn ngữ](#hỗ-trợ-đa-ngôn-ngữ)


## Giới thiệu

Tài liệu này cung cấp quy ước viết code cho BPAX Frontend, nhằm đảm bảo chất lượng và khả năng bảo trì của mã nguồn.

BPAX Frontend có cấu trúc micro-frontend sử dụng **single-spa**, bao gồm các repository chính sau:

- **web-root**: Cấu hình root (root config)・Proxy server
- **web-ui**: Ứng dụng chính (React SPA, đối tượng chính của quy ước này)
- **hr-web-ui** v.v.: Ứng dụng frontend do các team khác quản lý

Các mục trong phần [Định dạng](#định-dạng) được tự động sửa hoặc phát hiện lỗi, còn các mục khác ghi nhận những việc developer cần xử lý thủ công.

## Cấu trúc thư mục

Đối tượng ghi nhận là thư mục `src` trong thư mục gốc của dự án web-ui.

```
├── src
│   ├── api
│   │   ├── users.ts
│   │   └── workspaces.ts
│   ├── assets
│   │   ├── icon.svg
│   │   └── icon.png
│   ├── components
│   │   ├── button
│   │   │   └── Button.tsx
│   │   └── icon
│   │       └── Icon.tsx
│   ├── constants
│   │   ├── appConstants.ts
│   │   └── scaffoldConstants.ts
│   ├── css
│   │   └── style.css
│   ├── hooks
│   │   └── useLocalHistory.ts
│   ├── lib
│   │   ├── auth
│   │   │   └── auth.ts
│   │   ├── axios
│   │   │   └── axios.ts
│   │   └── http
│   │       └── useBpaxClient.ts
│   ├── pages
│   │   ├── taskList
│   │   │   └── TaskList.tsx
│   │   └── taskDetail
│   │       └── TaskDetail.tsx
│   ├── router
│   │   └── Router.ts
│   ├── stores
│   │   ├── userState.ts
│   │   └── workspaceState.ts
│   └── types
│       ├── users.ts
│       └── workspaces.ts
```

### Mô tả thư mục

#### api

Lưu trữ khai báo request của các API và api hook.

#### assets

Lưu trữ logo và các file hình ảnh (SVG, PNG) sử dụng trong ứng dụng.

#### components

Lưu trữ các UI component dùng chung (button, icon, v.v.). Thư mục sẽ tăng theo từng loại component (button, icon, v.v.).

#### constants

Lưu trữ các hằng số sử dụng trong toàn bộ ứng dụng hoặc trong page.

Việc chia file thực hiện theo đơn vị nhóm tùy ý.

#### css

Lưu trữ các utility class (global CSS) để chỉ định margin đơn lẻ hoặc text style.

#### hooks

Lưu trữ các custom hook.

Dự án BPAX sử dụng hook để tách biệt component và logic, giúp việc test dễ dàng hơn.

#### lib

Lưu trữ re-export của các thư viện bên ngoài được cấu hình sẵn cho ứng dụng (axios, v.v.) hoặc các xử lý tập trung của tính năng cụ thể (http, auth, v.v.).

#### pages

Lưu trữ các component của page. Thư mục sẽ tăng theo từng page.

#### router

Lưu trữ định nghĩa routing của react-router-dom.

#### stores

Lưu trữ các file liên quan đến Recoil.

atom và selector được khai báo trong cùng một file, và giá trị được truyền đến component thông qua custom hook.

#### types

Lưu trữ interface của dữ liệu request・response của API.


## Thông số file

Sử dụng file có mã ký tự `UTF-8`, mã xuống dòng `LF`.

## Định dạng

Các mục có tự động sửa `○` sẽ được tự động sửa khi lưu file.

Đối tượng là các file có đuôi `.js`, `.json`, `.ts`, `.tsx`.

| Mục                    | Công cụ kiểm tra | Tự động sửa | Mô tả                                                                                                           |
| :--------------------- | :--------------- | :---------- | :-------------------------------------------------------------------------------------------------------------- |
| Dấu ngoặc kép          | Prettier         | ○           | Sử dụng `dấu ngoặc đơn (')` trừ khi cần escape. Thuộc tính JSX sử dụng `dấu ngoặc kép (")`.                     |
| Thụt lề                | Prettier         | ○           | Sử dụng `2 dấu cách`.                                                                                           |
| Dấu chấm phẩy          | Prettier         | ○           | Sử dụng dấu chấm phẩy `;` ở cuối dòng.                                                                          |
| Số ký tự tối đa 1 dòng | Prettier         | ○           | `120` ký tự.                                                                                                    |
| JSX Bracket            | Prettier         | ○           | Nếu tag mở JSX có nhiều thuộc tính và nhiều dòng, đặt tag đóng `>` riêng trên dòng tiếp theo.                   |
| Thứ tự import          | Prettier         | ○           | Sắp xếp theo thứ tự: package bên ngoài → (xuống dòng) → module BPAX frontend (theo thứ tự alphabet).            |
| Dấu phẩy cuối          | Prettier         | ○           | Thêm dấu phẩy vào cuối tham số, mảng, object nhiều dòng.                                                        |
| Ngoặc arrow function   | Prettier         | ○           | Bắt buộc dấu ngoặc `()` ngay cả khi chỉ có 1 tham số. Ví dụ: `(x) => x`                                         |
| Khoảng trắng ngoặc     | Prettier         | ○           | Thêm khoảng trắng bên trong `{` `}` của object literal. Ví dụ: `{ foo: bar }`                                   |
| Ngoặc kép property     | Prettier         | ○           | Giữ nguyên ngoặc kép đã được thêm vào tên property của object.                                                  |
| Quy tắc đặt tên        | ESLint           | ×           | Quy tắc đặt tên theo từng mục sẽ được mô tả sau.                                                                |
| Mã xuống dòng          | ESLint           | ×           | Sử dụng `LF`.                                                                                                   |

## TypeScript

### Biến

Sử dụng `camelCase`.<br>
Câu lệnh khai báo sử dụng `const` hoặc `let`.

```tsx
// Bad
const UserName = '';
let first_name = '';

// Good
const userName = '';
let firstName = '';
```

### Hàm

Sử dụng `camelCase`.<br>
Định nghĩa hàm sử dụng `Arrow Functions`.

```tsx
// Bad
function getUserName() {
  return '';
}

// Good
const getUserName = () => {
  return '';
};
```

### Tên biến・Tên hàm

#### Quy tắc cơ bản

- Không sử dụng từ có nghĩa mơ hồ như `data` cho tên biến. Chỉ định từ rõ ràng.
    ```ts
    // Bad
    const getApplication = () => applicationId;
    const getApplicationData = () => applicationId;

    // Good
    const getApplicationId = () =>  applicationId;
    ```
- Khi viết tắt từ, chỉ viết hoa chữ cái đầu của mỗi từ gốc.
    ```ts
    // Bad
    userID
    getUri
    parseUrl

    // Good
    userId // Viết tắt của 1 từ Identification nên là Id
    getURI // Viết tắt của 3 từ Uniform Resource Identifier nên là URI
    parseURL // Viết tắt của 3 từ Uniform Resource Locator nên là URL
    ```
- Không viết tắt tên resource BPAX, ghi đầy đủ tên chính thức.
    ```ts
    // Bad
    // Tên biến
    const ws = {};
    const app = {};
    const ds = {};
    // Tên hàm
    const getWs = () => {};
    const updateApp = () => {};
    const deleteDs = () => {};
    // Tên component
    const WsList = () => {};
    const AppDetail = () => {};    

    // Good
    // Tên biến
    const workspace = {};
    const application = {};
    const datastore = {};
    // Tên hàm
    const getWorkspace = () => {};
    const updateApplication = () => {};
    const deleteDatastore = () => {};
    // Tên component
    const WorkspaceList = () => {};
    const ApplicationDetail = () => {};
    const DatastoreSettings = () => {};
    ```
- Sử dụng tên thống nhất trong toàn bộ source code. Khi thay đổi tên, tìm kiếm toàn bộ project để xác nhận phạm vi ảnh hưởng. Nếu ảnh hưởng nhiều file, hãy tạo PR riêng cho việc rename.
    ```ts
    interface User {
      userId: string;
      userName: string;
    }

    // Bad
    // UserList.tsx
    const UserList = () => {
      const accounts = useUsersQuery();
      return accounts.map(account => 
        <div>{account.name}</div>
      );
    };
    // UserDetail.tsx
    const UserDetail = () => {
      const member = useUserQuery();
      return <div>{member.name}</div>;
    };


    // Good
    // UserList.tsx
    const UserList = () => {
      const users = useUsersQuery();
      return users.map(user => 
        <div>{user.userName}</div>
      );
    };
    // UserDetail.tsx
    const UserDetail = () => {
      const user = useUserQuery();
      return <div>{user.userName}</div>;
    };
    ```
- Không sử dụng tùy tiện các prefix / suffix không được ghi trong quy ước này. Các prefix / suffix chính có thể sử dụng như sau:
  1. handle - event handler
  2. render - private component
  3. is / has / have / can / should - boolean
  4. use - hooks
  5. Request / Response - API types

  Nếu muốn sử dụng prefix / suffix khác, hãy xác nhận trước.
    ```ts
    // Bad
    // Prefix / suffix tùy ý:
    // prefix tmp
    const tmpData = {};
    // prefix my
    const myFunction = () => {};
    // suffix Impl
    class ServiceImpl {};
    // prefix do/exec
    const doSave = () => {};
    const execQuery = () => {};

    // Good
    // Prefix / suffix có thể sử dụng:
    // 1. handle cho event handler
    const handleClick = () => {};
    // 2. render cho private component
    const renderHeader = () => {};
    // 3. is/has/can/should cho boolean
    const isLoading = true;
    const hasError = false;
    // 4. use cho hooks
    const useCustomHook = () => {};
    // 5. Request/Response cho API types
    interface LoginRequest {}
    interface LoginResponse {}
    ```
- Lược bỏ thông tin có thể đọc được từ scope cha. Xác nhận mỗi lần xem có cần chỉ định tên biến dài không.
    ```tsx
    // Bad
    const App = () => {
      const appErrorMessage = "";
      const renderAppBody = () => <></>;
      return renderAppBody();
    }

    // Good
    const App = () => {
      const errorMessage = "";
      const renderBody = () => <></>;

      return renderBody();
    }
    ```
- Thống nhất thứ tự tên biến boolean: sau is/has/can/should là danh từ, rồi đến động từ/tính từ.
    ```js
    // Bad
    isDisabledButtonSave
    isOpenCSVSettings

    // Good
    isSaveButtonDisabled
    isCSVSettingsOpen
    ```
- Không đặt nhiều ý nghĩa cho tên event. Mỗi event handler chỉ xử lý một action. Xử lý phức tạp nên tách ra hàm riêng.
    ```tsx
    // Bad
    // Event handler chứa nhiều ý nghĩa
    <TextField
      onBlurSetValue={handleBlurSetValue}
      onChangeUpdateForm={handleChangeUpdateForm}
    />
    <Button onClickSaveAndClose={handleClickSaveAndClose} />

    // Good
    // Một event handler chỉ xử lý một action cụ thể
    <TextField
      onBlur={handleBlur}
      onChange={handleChange}
    />
    <Button onClick={handleSave} />
    ```


#### Event Handler

Tên hàm theo format: `handle` + `Event` + `Đối tượng (phần tử UI hoặc xử lý)`.

```tsx
// Bad
const handleSaveButtonClick = () => {}
<Button onClick={handleSaveButtonClick}>Lưu</Button>

// Good
const handleClickSaveButton = () => {}
<Button onClick={handleClickSaveButton}>Lưu</Button>
```

Nếu tên `Event` và `Đối tượng (phần tử UI hoặc xử lý)` trùng nhau, lược bỏ phần sau.

```tsx
// Bad
const handleCloseClose = () => {}
<Dialog onClose={handleCloseClose} />

// Good
const handleClose = () => {}
<Dialog onClose={handleClose} />
```

Khi chỉ định cùng một hàm cho nhiều event, chỉ định một trong các `Event`.<br>

```tsx
// Bad
const handleClickCloseButton = () => {}
<Dialog onClose={handleClickCloseButton} />
<Button onClick={handleClickCloseButton}>Đóng</Button>

// Good
const handleClose = () => {}
<Dialog onClose={handleClose} />
<Button onClick={handleClose}>Đóng</Button>
```

### Comment

Không sử dụng cú pháp `JSDoc`.<br>
Chỉ viết comment trong các trường hợp sau:

- Cơ bản chỉ cho business logic phức tạp
- Khi giải thích lý do xử lý tạm thời (giải pháp tạm thời thay vì giải quyết triệt để)

Thay vì viết comment, khuyến khích đặt tên biến・hàm dễ hiểu, chia nhỏ logic phức tạp, tận dụng type / interface.

```tsx
// Bad
/**
 * Tính tổng tiền đơn hàng
 * @param items Danh sách sản phẩm
 * @returns Tổng tiền
 */
const calculateTotal = (items: Item[]) => {
  return items.reduce((sum, item) => sum + item.price, 0);
};

// Good: Nội dung rõ ràng từ code, không cần comment
const getUserName = () => {
  return user.name;
};
```

### Kiểu dữ liệu

Nếu kiểu của biến được suy luận, lược bỏ type annotation.<br>
Nếu không suy luận được (any type), chỉ định kiểu.

```tsx
// Bad
const foo: string = '';
const bar: { name: string; age: number } = {
  name: 'suzuki',
  age: 20,
};

// Good
const foo = '';
const bar = {
  name: 'suzuki',
  age: 20,
};
```

### Class

Sử dụng `PascalCase`.<br>
Member và method sử dụng `camelCase`. Không thêm prefix cho private member.

```tsx
// Bad
class foo {
  Bar: string;
  _baz() {
    return '';
  }
}

// Good
class Foo {
  bar: string;
  baz() {
    return '';
  }
}
```

### Interface

Sử dụng `PascalCase`.<br>
Member sử dụng `camelCase`.<br>
Không sử dụng `I` làm prefix.

```tsx
// Bad
interface IFoo {
  Bar: string;
  Baz: number;
}

// Good
interface Foo {
  bar: string;
  baz: number;
}
```

Tên interface của API request/response theo format: `API path` + `Request` hoặc `Response`.<br>
Nếu API path hỗ trợ nhiều HTTP method, thêm HTTP method làm prefix (để tránh trùng tên interface).<br>
Nếu dữ liệu API request/response là kiểu mảng, không áp dụng quy tắc trên, chỉ định nghĩa kiểu của phần tử.

```tsx
// Bad
interface tokenAuthReq {}           // Không sử dụng camelCase・viết tắt
interface tokenAuthRes {}
interface WorkspacesRequest {}      // Nếu có cả GET・POST, cần prefix HTTP method
interface WorkspacesResponse {}

// Good
// Trường hợp /token_auth chỉ hỗ trợ POST
interface TokenAuthRequest {}
interface TokenAuthResponse {}

// Trường hợp /workspaces hỗ trợ cả GET・POST
interface GetWorkspacesRequest {}
interface GetWorkspacesResponse {}
interface PostWorkspacesRequest {}
interface PostWorkspacesResponse {}

// Trường hợp kiểu mảng, chỉ định nghĩa kiểu phần tử, phía gọi chỉ định kiểu mảng trong generics
interface Application {}
await http.getAsync<undefined, Application[]>(`workspaces/${workspaceId}/applications`);
```

### Type

Sử dụng `PascalCase`.<br>
Member sử dụng `camelCase`.

```tsx
// Bad
type foo = {
  Bar: string;
  Baz: string;
}
type userRole = 'admin' | 'user';

// Good
type Foo = {
  bar: string;
  baz: string;
}
type UserRole = 'admin' | 'user';
type HttpMethod = 'GET' | 'POST' | 'PUT';
```

### Interface vs Type

Sử dụng `interface` cho định nghĩa kiểu thông thường.<br>
Sử dụng `type` khi cần union type hoặc intersection type.<br>
Không sử dụng `type` cho định nghĩa object đơn giản.

```tsx
// Bad
// Không sử dụng type cho định nghĩa object đơn giản
type User = {
  id: string;
  name: string;
}

// Good
// Định nghĩa object thông thường dùng interface
interface User {
  id: string;
  name: string;
}

// Union type・intersection type dùng type
type UserRole = 'admin' | 'user';
type UserWithRole = User & {
  role: UserRole;
};
```

### Enum

Sử dụng `PascalCase`.<br>
Member sử dụng `camelCase`.

```tsx
// Bad (Member dùng PascalCase)
enum HttpStatusCode {
  BadRequest = 400,
  Unauthorized = 401,
}

// Good
enum HttpStatusCode {
  badRequest = 400,
  unauthorized = 401,
}
```

### null vs undefined

Trong code frontend sử dụng `undefined`. Không sử dụng `null`.

Tuy nhiên, có các trường hợp ngoại lệ sau:

- Khi `null` được trả về từ bên ngoài như API response
- Khi cần `null` theo spec API của thư viện bên thứ ba

```ts
// Bad
let user = null;                        // Không sử dụng null cho giá trị chưa khởi tạo
const result = value ?? null;           // Không sử dụng null cho fallback
setState({ data: null });               // Không sử dụng null cho state nội bộ

// Good
let user: User | undefined;            // Chưa khởi tạo là undefined (default của let)
const result = value ?? undefined;
setState({ data: undefined });

// OK (Ngoại lệ: null từ bên ngoài)
const apiUser = response.data;          // Xử lý nguyên nếu API response trả về null
const ref = useRef<HTMLDivElement>(null); // Trường hợp cần null theo spec API của thư viện
```

### Mảng

#### Định nghĩa kiểu

Sử dụng `[]`. Không sử dụng `Array`.

```tsx
// Bad
const items: Array<Item> = [];
const names: Array<string> = [];

// Good
const items: Item[] = [];
const names: string[] = [];
```

Khi kế thừa interface với mảng, sử dụng `Array`.

```
// Bad
export interface Foo extends Bar[] {}
// -> Parsing error: An element access expression should take an argument. eslint

// Good
export interface Foo extends Array<Bar> {}
```

#### Truy cập phần tử mảng

Sử dụng `array[index]`.

Chỉ khi truy cập phần tử cuối cùng, sử dụng `array.at(-1)`.<br>
Vì method at không kiểm tra tham số có phải số hay không, chỉ cho phép số literal.

```ts
const arr = [1, 2, 3, 4, 5];

// Bad
const firstNum = arr.at(0); // Không cần dùng at() cho phần tử đầu
const lastNum = arr[arr.length - 1]; // Phần tử cuối dùng at(-1)

// Good
const firstNum = arr[0];
const lastNum = arr.at(-1);
```

### Object

Khi tên key và tên biến giá trị giống nhau, sử dụng cú pháp shorthand. Áp dụng cho cả khai báo và tham số hàm.

```tsx
// Bad
const name = 'John';
const age = 20;
const user = { name: name, age: age };
updateUser({ name: name, age: age });

// Good
const name = 'John';
const age = 20;
const user = { name, age };
updateUser({ name, age });
```

### Rẽ nhánh điều kiện

Không lược bỏ block ({}) của if-else.

```ts
// Bad
if (!isOpen) return false;
else return true;

// Good
if (!isOpen) {
  return false;
} else {
  return true;
}
```

### Console log

Không sử dụng `console.xxxx`. Cũng không thêm log không cần thiết.

Khi cần, sử dụng `Logger` trong src/lib/logger.

```ts
// Bad
console.log('Debug info');
console.error('Error occurred');
console.warn('Warning message');
console.log('here');
console.log('data:', data);

// Good
import Logger from '@/lib/logger/logger';

Logger.console.error('API call failed', error);
Logger.console.info('Processing data', { count });
Logger.console.warn('Rate limit reached');
```

### Tên file

Đuôi .js, .ts sử dụng `camelCase`.<br>
Đuôi .tsx sử dụng `PascalCase` (để tên component và tên file khớp nhau).

```
// Bad
// File .js / .ts
UserUtils.ts
APIHelper.js
HTTPClient.ts

// File .tsx
userProfile.tsx
loginPage.tsx
dataTable.tsx

// Good
// File .js / .ts
userUtils.ts
apiHelper.js
constants.ts
httpClient.ts

// File .tsx
UserProfile.tsx
LoginPage.tsx
DataTable.tsx
```

### Import

Chỉ định bằng alias `@/` (`@/` tương ứng với `src/`). Không sử dụng đường dẫn tương đối (`../`, `./`).

```ts
// Bad
import { useApplicationsQuery } from '../../api/applications';
import Spacer from '../components/shared/spacer/Spacer';
import { Logger } from './lib/logger';

// Good
import { useApplicationsQuery } from '@/api/applications';
import Spacer from '@/components/shared/spacer/Spacer';
import { useBpaxClient } from '@/lib/http/useBpaxClient';
```

### Export

Sử dụng `named export` cho biến, hàm, Enum, interface.

```tsx
export const foo = '';
export const bar = () => {};
export enum Baz {}
export interface Qux {}
```

Sử dụng `default export` cho class. (Export component sẽ được mô tả sau)

```tsx
// Bad
// Không sử dụng default export cho thứ khác ngoài class
const apiPath = '/api';
export default apiPath;

// Không sử dụng named export cho class
export class Logger {
  log(message: string) {}
}

// Good
// Thứ khác ngoài class dùng named export
export const apiPath = '/api';

// Class dùng default export
class Logger {
  log(message: string) {}
}
export default Logger;
```

## React

### Component

Sử dụng `PascalCase` cho component được export (để tên file và tên component khớp nhau).<br>
Sử dụng Arrow Functions để định nghĩa function component. Không sử dụng class component.

Component không export sử dụng `camelCase` và có prefix `render`.

```tsx
// Bad
// Không sử dụng class component
class UserProfile extends React.Component {
  render() {
    return <div>User Profile</div>;
  }
}

// Không sử dụng PascalCase cho component không export
const App = () => {
  const Header = () => <header>Header</header>;
  return <div>{Header()}</div>;
};

// Good
// Component được export
const UserProfile = () => {
  return <div>User Profile</div>;
};
export default UserProfile;

// Component không export
const App = () => {
  const renderHeader = () => <header>Header</header>;
  const renderFooter = () => <footer>Footer</footer>;

  return (
    <div>
      {renderHeader()}
      <main>Main Content</main>
      {renderFooter()}
    </div>
  );
};
export default App;
```

### Khai báo biến

Khai báo biến theo thứ tự sau:

1. useParams
2. React Router Context wrapper hook
3. React hook (useState, useCallback, v.v.)
4. Hook bên thứ ba (useTranslation, useNavigate, v.v.)
5. Recoil wrapper hook (useXxxxState, v.v.)
6. Custom hook
7. Kiểm tra undefined của useParams
8. (Xuống dòng) React Query wrapper hook (useXxxxQuery, useXxxxMutation, v.v.)
9. (Xuống dòng) Kiểm tra undefined của React Query wrapper hook
10. (Xuống dòng) Custom hook phụ thuộc (trường hợp cần giá trị của hook trước làm input)
11. Các biến・hàm khác

```ts
// Bad: Thứ tự lộn xộn
const { t } = useTranslation();
const userQuery = useUserQuery();
const { userId } = useParams();
const [name, setName] = useState('');
const user = userQuery.data;
const { workspaceId } = useWorkspaceState();
const { permissions } = useUserPermissions();
const navigate = useNavigate();

// Good
// useParams
const { applicationId, taskId } = useParams();
// React Router Context wrapper hook
const { isOpen } = useXxxxContext();
// React hook (useState, useCallback, v.v.)
const [value, setValue] = useState("");
// Hook bên thứ ba (useTranslation, useNavigate, v.v.)
const { t } = useTranslation();
const navigate = useNavigate();
// Recoil wrapper hook (useXxxxState, v.v.)
const { currentWorkspaceId } = useWorkspaceState();
// Custom hook
const [isDrawerOpen, toggleIsDrawerOpen] = useToggle(true);
const previousPage = usePrevious(currentPage);
// Kiểm tra undefined của useParams
const currentApplicationId = applicationId ?? "";
const currentItemId = taskId ?? "";

// React Query wrapper hook (useXxxxQuery, useXxxxMutation, v.v.)
const datastoresQuery = useDatastoresQuery();
const loginMutation = useLoginMutation();

// Kiểm tra undefined của React Query wrapper hook
const datastores = datastoresQuery.data ?? [];

// Custom hook
const { currentPage } = useDataTable(currentDatastoreId);

// Các biến・hàm khác
...
...
```

### Event Handler

Khi tham số truyền từ event khớp với tham số của hàm, chỉ định trực tiếp hàm.<br>
Chỉ sử dụng arrow function khi cần tham số bổ sung.

```tsx
// Bad: Arrow function không cần thiết
const handleClick = () => {};
<Button onClick={() => handleClick()}>Click me</Button>

const handleChange = (event: ChangeEvent) => { setValue(event.target.value); };
<Input onChange={(event) => handleChange(event)} />

// Good: Truyền trực tiếp hàm
const handleClick = () => {};
<Button onClick={handleClick}>Click me</Button>

const handleChange = (event: ChangeEvent) => { setValue(event.target.value); };
<Input onChange={handleChange} />

// Good: Sử dụng arrow function khi cần tham số bổ sung
const handleDelete = (id: string) => { deleteItem(id); };
<Button onClick={() => handleDelete(item.id)}>Delete</Button>
```

### Import/Export Component

#### Import

Import với tên giống tên component.

```tsx
// Bad: Không import với tên khác tên component
import Profile from './UserProfile/UserProfile';
import Table from './DataTable/DataTable';

// Bad: Rename không cần thiết
import { Button as CustomButton } from './Button/Button';

// Good
import UserProfile from './UserProfile/UserProfile';
import DataTable from './DataTable/DataTable';
```

#### Export

Sử dụng default export. Viết riêng khai báo và export, 1 file = 1 component.

```tsx
// Bad: Không kết hợp khai báo và export
export default const Foo = () => {
  return <div></div>;
};

// Bad: Không sử dụng named export cho component
export const Foo = () => {
  return <div></div>;
};

// Good
const Foo = () => {
  return <div></div>;
};

export default Foo;
```

#### JSX Tag

Với component không có children, lược bỏ tag đóng và sử dụng self-closing tag.<br>
Khi có children thì sử dụng tag đóng.

```tsx
// Bad
<Dialog open></Dialog>
<Input value={value}></Input>
<Spinner size='large'></Spinner>

// Good
<Dialog open />
<Input value={value} />
<Spinner size='large' />

// Khi có children thì dùng tag đóng
<Button type='submit'>Submit</Button>
<Dialog open>
  <DialogTitle>Title</DialogTitle>
  <DialogContent>Content</DialogContent>
</Dialog>
```

#### Fragment

Sử dụng `<React.Fragment />`. Không sử dụng `<></>`.

Khi chỉ có một phần tử con, không sử dụng fragment.

Khi không render JSX thì return `null` (idiom chính thức của React). Không sử dụng `<React.Fragment />`.

```tsx
// Bad
// Không sử dụng fragment rút gọn
return (
  <>
    <Header />
    <MainContent />
    <Footer />
  </>
);

// Không cần fragment khi chỉ có 1 phần tử con
return (
  <React.Fragment>
    <MainContent />
  </React.Fragment>
);

// Không sử dụng React.Fragment khi không render JSX
if (!isOpen) return <React.Fragment />;

// Good
return (
  <React.Fragment>
    <Header />
    <MainContent />
    <Footer />
  </React.Fragment>
);

// Không cần fragment khi chỉ có 1 phần tử con
return <MainContent />;

// Khi không render JSX
if (!isOpen) return null;
```

#### Hook

Vì kiểu suy luận chính xác cho giá trị primitive, không chỉ định kiểu generics.<br>
Với kiểu phức tạp (union types, custom interface, kiểu chứa undefined) thì chỉ định kiểu generics.

```tsx
// Bad: Không cần kiểu generics cho giá trị primitive
const [value, setValue] = useState<string>("");
const [num, setNum] = useState<number>(0);
const [isOpen, setIsOpen] = useState<boolean>(false);

// Good: Giá trị primitive
const [value, setValue] = useState("");
const [num, setNum] = useState(0);
const [isOpen, setIsOpen] = useState(false);

// Good: Chỉ định kiểu generics cho kiểu phức tạp
const [user, setUser] = useState<User | undefined>(undefined);
const [items, setItems] = useState<Item[]>([]);
const [config, setConfig] = useState<Config>({
  theme: 'light',
  lang: 'en',
});
```

### Định nghĩa kiểu liên quan đến React

#### Import kiểu

Sử dụng default import, truy cập kiểu qua `React.` như `React.FC`, `React.ReactNode`. Không sử dụng named import (`{ FC }`, v.v.) hoặc namespace import (`* as`).

```tsx
// Bad
import { FC, ReactNode } from 'react';
import * as React from 'react';
import React, { FC, ReactNode, MouseEvent } from 'react';

// Good
import React from 'react';
```

#### Định nghĩa kiểu Component

Component có props sử dụng `React.FC<T>`.<br>
Không sử dụng `React.VFC<T>` vì đã deprecated.<br>
Component không có props thì lược bỏ định nghĩa kiểu.

```tsx
// Bad
// Không sử dụng VFC (deprecated)
const Button: React.VFC<ButtonProps> = (props) => {
  return <button>{props.label}</button>;
};

// Không sử dụng FC cho component không có props
const Header: React.FC = () => {
  return <header>App Header</header>;
};

// Không định nghĩa kiểu props inline
const Button: React.FC<{
  onClick: () => void;
  label: string;
}> = (props) => {
  return <button>{props.label}</button>;
};

// Good
// Có props
interface ButtonProps {
  onClick: () => void;
  label: string;
}

const Button: React.FC<ButtonProps> = ({ onClick, label }) => {
  return <button onClick={onClick}>{label}</button>;
};

// Không có props
const Header = () => {
  return <header>App Header</header>;
};
```

#### Định nghĩa kiểu props

Đặt tên là Tên component + `Props`.

```tsx
// Bad
interface IButtonProps {...}       // Không cần prefix I
interface ButtonPropsType {...}    // Không cần suffix Type
interface ButtonInterface {...}    // Không cần suffix Interface
// Tên component và tên props không khớp
interface SubmitButtonProps {...}
const Button: React.FC<SubmitButtonProps> = (props) => {...}

// Good
interface ButtonProps {
  onClick: () => void;
  label: string;
}
const Button: React.FC<ButtonProps> = (props) => {...}
```

### Cách nhận props

Sử dụng destructuring.

```tsx
// Bad
const Foo: React.FC<FooProps> = (props) => {
  return <div></div>;
};

// Good
const Foo: React.FC<FooProps> = ({ bar, baz }) => {
  return <div key={bar}>{baz}</div>;
};

// Good
// Khi truyền props còn lại xuống component con
const Foo: React.FC<FooProps> = ({ bar, baz, ...props }) => {
  return <div key={bar} {...props}>{baz}</div>;
};
```

## Phương hướng xử lý lỗi

### Lỗi API (đã xác thực)

Khi xảy ra status code 4XX, 5XX, sử dụng xử lý lỗi chung sau:<br>

```ts
// Xử lý lỗi chung (hàm trong useBpaxClient.ts/useHexabaseClient.ts)
const handleErrorAPIResponse = (error: any) => {
  if (axios.isAxiosError(error)) {
    if (error.response) {
      const { status } = error.response;
      switch (status) {
        case HttpStatusCode.unauthorized:
          logout();
          break;
        default:
          // Hiển thị snackbar của package notistack
          enqueueSnackbar(t('enqueueSnackbar.somethingWentWrong'));
          break;
      }
    }
  }
};
```

| Status Code | Xử lý lỗi                                                                                                       |
| :---------- | :-------------------------------------------------------------------------------------------------------------- |
| 401         | Logout                                                                                                          |
| Còn lại     | Hiển thị snackbar package `notistack` ở góc dưới phải màn hình<br>(Thông báo lỗi: Đã xảy ra lỗi không mong đợi) |

Chỉ định xử lý lỗi chung `handleErrorAPIResponse` như sau:
- `useQuery`: Chỉ định trong `meta.onError`
- `useMutation`: Chỉ định trực tiếp trong `onError`

```ts
// Bad: Không xử lý lỗi riêng lẻ
const useDatastoreQuery = (id: string) => {
  return useQuery({
    queryKey: [QueryKey.datastore, id],
    queryFn: async () => {
      try {
        const res = await axios.get(`/api/datastores/${id}`);
        return res.data;
      } catch (error) {
        if (error.response?.status === 401) {
          logout();
        } else {
          alert('Error occurred');
        }
      }
    },
  });
};

// Bad: Không có xử lý lỗi
const useDatastoreQuery = (id: string) => {
  return useQuery({
    queryKey: [QueryKey.datastore, id],
    queryFn: () => fetch(`/api/datastores/${id}`),
  });
};

// Good: useQuery chỉ định trong meta.onError
export const useDatastoreActionsQuery = (datastoreId: string) => {
  const { http, handleErrorAPIResponse } = useBpaxClient();
  return useQuery({
    queryKey: [QueryKey.actions, datastoreId],
    queryFn: async () => {
      const res = await http.getAsync<undefined, Actions>(`datastores/${datastoreId}/actions`);
      return res.data;
    },
    meta: {
      onError: handleErrorAPIResponse,
    },
    enabled: !!datastoreId,
    ...getSettingCacheTime(),
  });
};

// Good: useMutation chỉ định trực tiếp trong onError
export const useUpdateDatastoreMutation = () => {
  const { http, handleErrorAPIResponse } = useBpaxClient();
  return useMutation({
    mutationFn: async (params: UpdateDatastoreParams) => {
      const res = await http.putAsync<UpdateDatastoreParams, DataStore>(
        `datastores/${params.id}`,
        params,
      );
      return res.data;
    },
    onError: handleErrorAPIResponse,
  });
};
```

### Lỗi API (chưa xác thực)

Đối tượng là Login API, Password Reset API, Account Registration API, v.v.<br>
Vì là API khi chưa xác thực, không cần sign out của xử lý lỗi chung.

Do đó, không sử dụng xử lý lỗi chung mà chỉ định xử lý lỗi theo yêu cầu.

```ts
// Bad: Không sử dụng xử lý lỗi chung cho API chưa xác thực
const useLoginMutation = () => {
  const { handleErrorAPIResponse } = useBpaxClient();
  return useMutation({
    mutationFn: async (credentials) => {
      const res = await axios.post('/api/login', credentials);
      return res.data;
    },
    onError: handleErrorAPIResponse,
  });
};

// Good: Xử lý lỗi riêng theo yêu cầu
const useLoginMutation = () => {
  return useMutation({
    mutationFn: async (credentials) => {
      const res = await axios.post('/api/login', credentials);
      return res.data;
    },
    onError: (error) => {
      if (axios.isAxiosError(error)) {
        const status = error.response?.status;
        if (status === 400) {
          enqueueSnackbar('Invalid credentials', { variant: 'error' });
        } else {
          enqueueSnackbar('Login failed', { variant: 'error' });
        }
      }
    },
  });
};
```

### Lỗi JavaScript (xử lý ngoại lệ)

Xử lý bằng `ErrorBoundary` ở root component.<br>
Khi bắt được lỗi, hiển thị component được chỉ định trong option `FallbackComponent`.

```tsx
const App = () => (
  <QueryClientProvider client={queryClient}>
    <ReactQueryDevtools initialIsOpen={false} />
    <ThemeProvider theme={theme}>
      <SnackbarProvider>
        <CssBaseline enableColorScheme />
        <RecoilRoot>
          {/* Bắt exception xảy ra dưới ErrorBoundary và hiển thị fallback UI */}
          <ErrorBoundary FallbackComponent={ErrorFallback}>
            <Router />
          </ErrorBoundary>
        </RecoilRoot>
      </SnackbarProvider>
    </ThemeProvider>
  </QueryClientProvider>
);
```

## Styling

- Sử dụng CSS Modules cho local style.
- Khi chỉ định margin đơn lẻ hoặc text style, sử dụng utility class (global CSS) (src/css/style.css)
- Về nguyên tắc không hỗ trợ responsive. Màn hình cần hỗ trợ sẽ được ghi rõ khi yêu cầu task.
- Không chỉ định tên class CSS Modules sau khi chuyển đổi trong selector. Vì có thể bỏ sót khi thay đổi tên class.

```tsx
// Bad: Không chỉ định trực tiếp tên class CSS Modules sau khi chuyển đổi
const Button = () => (
  <button className="Button_button__1a2b3">Click me</button>
);

// Good: CSS Modules
// Button.module.css
// .button { background-color: blue; color: white; }
import styles from './Button.module.css';
const Button = () => (
  <button className={styles.button}>Click me</button>
);

// Good: Global CSS (utility class)
// src/css/style.css
// .text-center { text-align: center; }
const App = () => (
  <div className="text-center">Welcome</div>
);
```

## Bảo mật (thông tin bí mật)

BPAX Frontend không quản lý thông tin bí mật (secret key, API key, password, token bí mật, v.v.).<br>
Khi sử dụng secret key, quản lý ở backend.

Google Analytics, Sentry, v.v., những thứ được service chỉ định quản lý bằng JavaScript là ngoại lệ.

## Hỗ trợ đa ngôn ngữ

Văn bản được định nghĩa trong file từ điển `lib/i18n/locales/${language}.json`.

Hiện tại chỉ hỗ trợ tiếng Nhật.

Quy tắc key trong file từ điển như sau:

- Tên key sử dụng `camelCase`.
- Root key chỉ định tên component (sau khi chuyển đổi sang camelCase).
  - Nếu có component tương tự, sử dụng tên khác để thống nhất.
- Nếu có 2 mục trở lên có thể nhóm lại, nhóm bằng tên key chung (menus, forms, v.v.).
- Khi chỉ định tên key cho phần tử không được nhóm, đặt tên key là tên mục (account, tokenAuth, v.v.) + tên có thể phân biệt phần tử UI (errorMessage, linkText, v.v.).
- Chú ý không khác biệt với cấu trúc key của component khác.


`Bad`
```json
// Không sử dụng snake_case / kebab-case
{
  "app_bar": {
    "account-menu": {
      "sign_out": "Sign out"
    }
  }
}

// Không tách rời cấu trúc
{
  "appBar": {
    "signOut": "Sign out"
  },
  "accountMenu": {
    "signOut": "Sign out"
  }
}

// Thiếu nhóm
{
  "portalLink": "Portal",
  "dashboardLink": "Dashboard",
  "settingsLink": "Settings"
}
```

`Good`
```json
{
  "appBar": {
    "accountMenu": {
      "signOut": "Đăng xuất"
    }
  },
  "drawer": {
    "menus": {
      "portal": "Portal",
      "creation": "Tạo mới",
      "businessProcess": "Quy trình nghiệp vụ",
      "dashboard": "Dashboard",
      "processSetting": "Cài đặt quy trình"
    }
  },
  "portal": {
    "title": "Portal"
  },
  "signIn": {
    "title": "Đăng nhập",
    "forms": {
      "signIn": "Đăng nhập",
      "email": "Email",
      "password": "Mật khẩu"
    },
    "tokenAuthErrorMessage": "Email hoặc mật khẩu không chính xác.",
    "passwordRecoverLinkText": "Quên mật khẩu? Nhấn vào đây",
    "signUpLinkText": "Chưa có tài khoản? Nhấn vào đây"
  }
}
```