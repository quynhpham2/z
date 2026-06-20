# Kịch bản trình bày — Bảo vệ đồ án tốt nghiệp

> **Đối tượng:** Hội đồng phản biện (giảng viên, lớn tuổi hơn — millennial).
> **Phong cách:** Thân thiện, tự tin nhưng khiêm tốn. Dùng "em" với hội đồng. Tránh quá nhiều thuật ngữ kỹ thuật khô khan.
> **Thời lượng:** ~10 phút trình bày + Q&A.
> **Trọng tâm:** Introduction → Problem → Architecture → **Challenges (slide 9)** → Conclusion & Discussion.
> **Skim nhanh:** Sơ đồ luồng (slide 6–8) và Demo (slide 10–13) — chỉ chỉ tay, mô tả 1–2 câu, không sa đà.
> **Mẹo:**
> - Mở đầu bằng câu chuyện thực tế, không sa đà vào định nghĩa.
> - Khi đến slide 9 (challenges) thì **chậm lại, đầu tư thời gian** — đây là phần thể hiện chiều sâu kỹ thuật.
> - Nếu thầy cô hỏi giữa chừng: trả lời ngắn rồi quay lại slide, đừng phá nhịp.

---

## Slide 1 — Title (≈ 30s)

> "Em xin kính chào quý Thầy Cô trong hội đồng. Em tên là **Nguyễn Đỗ Quang Huy**, mã số sinh viên **59130946**, dưới sự hướng dẫn của **Cô Phạm Thị Kim Ngoan**.
>
> Hôm nay em xin được trình bày đồ án tốt nghiệp với đề tài: **Xây dựng ứng dụng đặt lịch hẹn dịch vụ trên thiết bị di động**.
>
> Bài trình bày của em tập trung vào 4 phần: **bối cảnh & vấn đề — kiến trúc hệ thống — khó khăn kỹ thuật & cách giải quyết — tổng kết và thảo luận**. Phần sơ đồ luồng và demo em xin lướt nhanh để dành thời gian cho thảo luận. Em xin phép bắt đầu."

---

## Slide 2 — Vấn đề & Lý do chọn đề tài (≈ 75s) ⭐

> "Thưa Thầy Cô, em chọn đề tài này xuất phát từ một quan sát thực tế ở Việt Nam: phần lớn các cửa hàng nhỏ — như **spa, salon tóc, chăm sóc thú cưng, sửa chữa** — vẫn quản lý lịch hẹn rất thủ công: gọi điện, nhắn Zalo, hoặc ghi sổ tay.
>
> Cách làm này tạo ra ba khoảng trống:
> - **Phía khách hàng:** không biết khung giờ nào trống, phải gọi đi gọi lại để xác nhận, không có nơi lưu lại lịch sử dịch vụ.
> - **Phía chủ cửa hàng:** rất dễ trùng lịch, đặc biệt khi nhiều nhân viên cùng nhận khách; không có cảnh báo real-time.
> - **Giải pháp hiện có:** app nước ngoài như Booksy hay Fresha rất tốt, nhưng **phí cao, chưa Việt hoá**, không phù hợp ngữ cảnh hộ kinh doanh nhỏ ở Việt Nam.
>
> Vì vậy em mong muốn xây dựng một sản phẩm **phù hợp hơn cho thị trường Việt Nam**."

---

## Slide 3 — Mục tiêu nghiên cứu (≈ 60s) ⭐

> "Mục tiêu chính của đề tài là xây dựng một ứng dụng di động **hai vai trò**: khách hàng và chủ cửa hàng — đồng bộ thông tin với nhau real-time.
>
> Về ý tưởng cốt lõi, em mượn hai concept quen thuộc:
> - **Airbnb** giúp cá nhân cho thuê nhà / phòng.
> - **Shopee** giúp shop nhỏ bán hàng online.
>
> Ý tưởng của em tương tự: giúp **hộ kinh doanh nhỏ** quản lý lịch hẹn ngay trên điện thoại. Nhiều chủ cửa hàng cảm thấy mở laptop để quản lý là *quá overkill* — họ muốn sự tiện lợi của app: mọi thứ trong tầm tay, mọi lúc mọi nơi.
>
> Còn phía khách hàng thì có app riêng để **tìm kiếm dịch vụ xung quanh** và đặt lịch — giống cách họ dùng Google Maps để tìm quán ăn."

---

## Slide 4 — Nghiên cứu liên quan (≈ 60s)

> "Em đã khảo sát ba app phổ biến: **Booksy, Fresha và GoBeauty**.
>
> Nhìn vào bảng — Booksy và Fresha mạnh về kỹ thuật nhưng nhắm tới salon chuyên nghiệp ở Mỹ / châu Âu, phí cao; GoBeauty có tiếng Việt nhưng thiếu nhiều tính năng cốt lõi.
>
> Điểm khác biệt của đề tài em nằm ở **định vị thị trường** — em không cạnh tranh tính năng kỹ thuật mà nhắm vào **ngách chưa được phục vụ tốt**: hộ kinh doanh nhỏ tại Việt Nam, miễn phí, mobile-first, hỗ trợ nhiều dịch vụ trong một cửa hàng, kèm QR check-in và moderation review phù hợp ngữ cảnh Việt."

---

## Slide 5 — Kiến trúc hệ thống (≈ 75s) ⭐

> "Về kiến trúc, hệ thống được chia thành **3 tầng**:
>
> - **Tầng 1 — Clients:** Hai ứng dụng mobile React Native + Expo cho khách hàng và chủ cửa hàng, cùng web admin (React + Vite) cho vận hành hệ thống.
> - **Tầng 2 — Backend:** REST API viết bằng **NestJS** (Node.js + TypeScript), đóng vai trò *single source of truth*.
> - **Tầng 3 — Data & External services:** PostgreSQL làm cơ sở dữ liệu chính, Firebase Auth để xác thực, Firebase Cloud Messaging để gửi push notification.
>
> Mọi giao tiếp đều qua **HTTPS**, xác thực bằng **JWT** do Firebase Auth phát hành — backend chỉ *verify token* mà không lưu mật khẩu, giảm rủi ro bảo mật.
>
> Kiến trúc này đơn giản, dễ deploy trên Render hay Railway — phù hợp ngân sách của hộ kinh doanh nhỏ, đúng nhóm khách hàng mục tiêu."

---

## Slide 6 — Sơ đồ luồng: Tổng quan & Onboarding (≈ 25s — *skim*)

> "Slide này em chỉ lướt qua hai luồng cơ bản: **điều hướng tổng quan** giữa hai vai trò, và **quy trình onboarding cửa hàng 5 bước** — chuyển một khách hàng phổ thông thành chủ cửa hàng trong vài phút. Chi tiết em đã ghi trong báo cáo, em xin phép đi tiếp."

---

## Slide 7 — Sơ đồ luồng: Khách hàng (≈ 20s — *skim*)

> "Tương tự, đây là luồng phía khách hàng: **tìm kiếm → đặt lịch → check-in → đánh giá**. Em xin lướt nhanh."

---

## Slide 8 — Sơ đồ luồng: Quản lý cửa hàng (≈ 20s — *skim*)

> "Và đây là luồng phía chủ cửa hàng: **lưới lịch — danh sách lịch hẹn — cài đặt cửa hàng — quét QR check-in**. Em sẽ nói kỹ về lưới lịch ở slide tiếp theo."

---

## Slide 9 — Khó khăn gặp phải (≈ 150s) ⭐⭐⭐

> "Đây là phần em xin đầu tư thời gian nhất, vì nó thể hiện chiều sâu kỹ thuật của đồ án. Em đã liệt kê 6 khó khăn trọng tâm và cách giải quyết.
>
> **1. Tag & Filter — phân loại ngành đa cấp.**
> Một cửa hàng có thể thuộc nhiều ngành, nhiều dịch vụ, nhiều tag. Nếu viết naive sẽ rơi vào **N+1 query** — mỗi cửa hàng lại bắn thêm 1 query để lấy tag. Em xử lý bằng *junction table* `store_tags` có composite index, và TypeORM QueryBuilder ghép động `andWhere` khi user chọn nhiều filter — toàn bộ chỉ trong 1 JOIN.
>
> **2. RBAC & Authorization.**
> Đây là lỗ hổng **OWASP A01 — Broken Access Control**, phổ biến nhất hiện nay, đặc biệt là dạng *IDOR* khi truy cập theo ID. Em dùng `@Roles()` decorator + `RolesGuard` của NestJS đọc claim từ JWT, **cộng thêm** resource-level check ở service layer — phải đúng owner mới được sửa cửa hàng. Em tách rõ: *Firebase là identity, backend là authorization* — frontend không bao giờ tự quyết quyền.
>
> **3. Race condition — double-booking & multi-edit cùng lịch hẹn.**
> Có hai tình huống thực tế: *(a)* hai khách tap đặt cùng một slot ở mili-giây cuối, *(b)* chủ và nhân viên cùng cập nhật trạng thái 1 lịch hẹn trên hai thiết bị khác nhau — kinh điển là **lost update**, người sau ghi đè người trước.
>
> Em chọn **optimistic locking** ở backend: entity có cột `version`, mỗi `UPDATE` đều kèm `WHERE version = ?` và tăng version lên 1. Nếu version không khớp thì backend throw `409 Conflict`, client refetch dữ liệu mới rồi merge. Em chọn optimistic thay vì pessimistic lock vì xung đột thực tế rất ít — không đáng để khóa row gây nghẽn DB.
>
> **4. Review & booking spam abuse.**
> Hai dạng tấn công: bot/đối thủ spam review xấu để bóp méo uy tín cửa hàng nhỏ, và user tạo hàng loạt booking giả để DoS chiếm hết slot. Em xử lý nhiều lớp: review chỉ tạo từ booking đã `completed` (gắn 1-1), rate-limit theo user và IP, kèm report system & moderation queue cho admin.
>
> **5. Map Integration Layer.**
> Geocoding API có rate-limit và quota. Nếu user pan bản đồ liên tục thì reverse-geo bắn request liên tục. Em wrap `expo-location` trong adapter, debounce 400ms, kèm LRU cache; mỗi địa chỉ lưu cả `lat/lng` lẫn `formatted_address` để khỏi phải reverse-geo lại.
>
> **6. Schedule Grid kéo–thả.**
> Vấn đề khó nhất là **gesture conflict**: cùng một bề mặt vừa cần kéo lịch hẹn, vừa cần cuộn trang. Em dùng `react-native-gesture-handler` với *simultaneous handler resolution*, snap-to-grid 15 phút, memoize từng ô lưới, và optimistic UI — di chuyển ngay, rollback nếu backend reject.
>
> Tổng kết slide này: đồ án **không đột phá công nghệ**, nhưng **lựa chọn có lý do** giữa các phương án — như chọn optimistic thay vì pessimistic locking — và kết hợp có hệ thống các kỹ thuật phổ biến để giải bài toán thực tế."

---

## Slide 10–12 — Demo (≈ 30s tổng — *skim*)

> "Em xin lướt nhanh qua các màn hình chính để Thầy Cô hình dung sản phẩm:
> - *Slide 10:* phía khách hàng — khám phá, bản đồ, chi tiết cửa hàng, chọn khung giờ.
> - *Slide 11:* sau khi đặt lịch — calendar cá nhân, QR check-in, đánh giá, đăng ký mở cửa hàng.
> - *Slide 12:* phía chủ cửa hàng — lưới lịch kéo–thả, chi tiết & chuyển trạng thái, cài đặt cửa hàng.
>
> Em có video demo chi tiết em sẵn sàng chiếu nếu Thầy Cô muốn xem ở phần Q&A."

---

## Slide 13 — Admin UI (≈ 15s — *skim*)

> "Ngoài app mobile em còn có web admin để vận hành: quản lý người dùng, kiểm duyệt cửa hàng, xử lý báo cáo. Em chọn web cho admin vì khối lượng dữ liệu lớn và thao tác bảng nhiều — desktop phù hợp hơn mobile."

---

## Slide 14 — Hạn chế & Hướng phát triển (≈ 60s)

> "Em xin thẳng thắn nhìn nhận các **hạn chế**:
> - Chưa tích hợp **cổng thanh toán online** (VNPay, Momo, SePay).
> - Bản đồ chưa có **chỉ đường**.
> - **Chưa có người dùng thực tế** để đánh giá sâu — đây là hạn chế lớn nhất.
> - UI còn cần thời gian polish.
>
> **Hướng phát triển** em hình dung:
> - Tích hợp **thanh toán & đặt cọc** để chống no-show.
> - **Analytics dashboard** giúp chủ cửa hàng hiểu doanh thu, peak hours.
> - Đồng bộ với **Google Calendar / Apple Calendar**.
> - **Hệ thống gợi ý** và **in-app chat** giữa khách và cửa hàng."

---

## Slide 15 — Tổng kết & Bước tiếp theo (≈ 75s) ⭐⭐

> "Em xin chốt lại, và đây là điều em muốn Thầy Cô lưu ý nhất.
>
> Đề tài của em **không đặt mục tiêu đột phá công nghệ** — em hoàn toàn ý thức điều này. Thay vào đó, em tập trung vào hai mục tiêu:
>
> 1. **Xây dựng một sản phẩm hoàn chỉnh** — đầy đủ 2 vai trò, hoạt động trên cả iOS và Android, đa ngôn ngữ, có web admin đi kèm, **sẵn sàng triển khai**.
> 2. **Tuân theo quy trình phát triển phần mềm thực tế** — đi đủ các bước *phân tích → thiết kế → hiện thực → kiểm thử → triển khai*, viết tài liệu, quản lý Git, CI/CD — như một dự án phần mềm thật ngoài doanh nghiệp.
>
> **Bước tiếp theo** của em là **thu hút một vài hộ kinh doanh nhỏ dùng thử** sản phẩm, lắng nghe phản hồi thực tế, và *iterate* sản phẩm theo nhu cầu thị trường. Em tin đây là cách duy nhất để một sản phẩm phần mềm trưởng thành."

---

## Slide 16 — Cảm ơn & Q&A (≈ 20s)

> "Bài trình bày của em đến đây là kết thúc. Em xin chân thành cảm ơn quý Thầy Cô đã lắng nghe, và đặc biệt cảm ơn **Cô Phạm Thị Kim Ngoan** đã hướng dẫn em trong suốt thời gian thực hiện đồ án.
>
> Em rất mong nhận được nhận xét và câu hỏi từ Hội đồng để hoàn thiện đồ án. Em xin lắng nghe ạ."

---

## Phụ lục — Câu hỏi có thể được hỏi & gợi ý trả lời

### 1. "Tại sao em chọn React Native thay vì native Android/iOS?"
> Em chọn React Native + Expo vì: (1) đề tài cần triển khai **đồng thời 2 nền tảng** với một developer; (2) Expo cho phép em build và OTA update nhanh, phù hợp giai đoạn iterate; (3) hệ sinh thái Map / Calendar đã chín muồi. Native sẽ cho hiệu năng tốt hơn nhưng overkill so với scope đề tài.

### 2. "Tại sao optimistic locking mà không pessimistic?"
> Hai lý do: (1) xung đột thực tế rất ít — đa số UPDATE không xảy ra cùng lúc; pessimistic lock sẽ khoá row không cần thiết, gây nghẽn DB khi scale. (2) optimistic dễ debug hơn vì xung đột trả về `409 Conflict` rõ ràng, client có thể hiện UI thông báo "dữ liệu đã thay đổi, refetch?" — UX tốt hơn là user chờ lock được giải phóng mà không biết tại sao.

### 3. "Nếu hai khách cùng đặt một khung giờ thì sao?"
> Cùng cơ chế optimistic locking — request thứ hai gặp version mismatch, backend trả `409`, app gợi ý khung giờ gần nhất. Cộng thêm composite unique constraint `(store_id, time_slot)` ở DB làm tầng phòng vệ cuối.

### 4. "RBAC khác authentication chỗ nào?"
> Authentication là *"bạn là ai"* — Firebase Auth xử lý. Authorization (RBAC) là *"bạn được làm gì"* — backend của em xử lý. JWT chỉ chứng minh danh tính; mỗi endpoint mới quyết định có cho phép hay không, dựa trên role và resource ownership.

### 5. "Em đo lường thành công của đề tài như thế nào?"
> Hai mức: (1) **kỹ thuật** — sản phẩm chạy ổn định trên cả 2 nền tảng, đầy đủ luồng nghiệp vụ, tài liệu hoá đầy đủ; (2) **thực tế** — đây là phần em đang ở bước đầu, cần dùng thử với hộ kinh doanh nhỏ để có dữ liệu định lượng (số booking thành công, tỉ lệ no-show, NPS).

### 6. "So với các app đã có, đề tài em đóng góp gì mới?"
> Em không cạnh tranh về tính năng kỹ thuật. Đóng góp chính là **định vị thị trường** chưa được phục vụ tốt — hộ kinh doanh nhỏ Việt Nam — và **kết hợp** các kỹ thuật phổ biến thành một sản phẩm hoàn chỉnh, miễn phí, mobile-first.

### 7. "Tại sao chọn PostgreSQL?"
> Vì dữ liệu có quan hệ rõ ràng (User — Store — Service — Booking — Review), và cần các tính năng như **transaction**, **constraint** để đảm bảo không trùng lịch. PostgreSQL cũng hỗ trợ tốt geo query nếu mở rộng tìm kiếm theo khoảng cách.

### 8. "Em mất bao lâu để hoàn thành đồ án?"
> Trả lời theo timeline thực tế — kèm chia giai đoạn (research, design, implement, test).
