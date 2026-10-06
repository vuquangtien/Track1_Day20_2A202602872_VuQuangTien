# Metrics Pack — AI Personal Assistant for Students

## 00 — Dự án, persona, core job

- **Dự án:** AI Personal Assistant for Students — trợ lý giúp sinh viên gom đầu việc học, ưu tiên chúng và lập kế hoạch học tập.
- **Persona:** Sinh viên đại học năm 1–3, học nhiều môn trong một học kỳ và tự quản lý deadline.
- **Core job:** “Tôi muốn biết việc học nào cần làm trước và hoàn thành chúng đúng hạn, thay vì bỏ sót deadline vì thông tin nằm rải rác ở nhiều nơi.”

## 01 — Core Action

### Phân biệt bốn khái niệm

| Khái niệm | Câu trả lời |
| --- | --- |
| Core job | Không bỏ sót việc học quan trọng và hoàn thành đúng hạn. |
| Core action | Hoàn thành một nhiệm vụ học tập đã được AI đưa vào kế hoạch. |
| Core value | Biết việc cần ưu tiên và tiến độ học tập thực sự đi đúng hạn. |
| Core value event | Nhiệm vụ trong kế hoạch được chuyển sang hoàn thành trước hoặc đúng deadline. |

### Core Action Card

| Thành phần | Câu trả lời |
| --- | --- |
| Target user | Sinh viên đại học tự quản lý deadline môn học. |
| Core job | Hoàn thành các việc học quan trọng đúng hạn mà không phải tự gom và sắp xếp thủ công. |
| Core action | Hoàn thành và xác nhận hoàn thành một nhiệm vụ học tập đã được AI lập kế hoạch. |
| Object | Một `study_task` có deadline và có mặt trong kế hoạch học tập. |
| Preconditions | Sinh viên đã có tài khoản; đã thêm/đồng bộ nhiệm vụ; nhiệm vụ có deadline; AI đã đưa nhiệm vụ vào kế hoạch và sinh viên xác nhận kế hoạch. |
| Completion rule | Nhiệm vụ đổi trạng thái từ `incomplete` sang `completed`; thời điểm hoàn thành không muộn hơn `due_at`. |
| Core value | Sinh viên tiến gần mục tiêu học tập, biết ưu tiên có hiệu quả và tránh trễ hạn. |
| Evidence of value | Có ít nhất một nhiệm vụ trong kế hoạch được hoàn thành đúng hạn. |
| Candidate event | `planned_task_completed_on_time` |

### Tự kiểm 5 tiêu chí

| Tiêu chí | Đánh giá | Lý do |
| --- | --- | --- |
| Gần core value | Đạt | Hoàn thành đúng hạn là kết quả trực tiếp của việc ưu tiên và lập kế hoạch. |
| Có thể lặp lại | Đạt | Deadline và bài tập mới xuất hiện liên tục trong học kỳ. |
| Có thể quan sát | Đạt | Có task ID, trạng thái chuyển đổi và thời điểm hoàn thành/deadline. |
| Có ý nghĩa | Đạt | Nhiều nhiệm vụ đã lên kế hoạch hoàn thành đúng hạn phản ánh giá trị thực, không chỉ hoạt động trong app. |
| Có thể tác động | Đạt | Team có thể cải thiện việc nhập nhiệm vụ, chất lượng ưu tiên và kế hoạch theo thời gian thực. |

**Kết quả Gate 1:** 5/5. Đây không phải “mở app” hay “hỏi AI”: hai thao tác đó chưa chứng minh sinh viên đã giải quyết được việc học.

## 02 — Action Nature Card + kết luận cadence

| Thành phần | Câu trả lời |
| --- | --- |
| Actor | Một sinh viên. |
| Intent | Tránh bỏ sót deadline và hoàn tất việc học quan trọng. |
| Trigger | Deadline môn học, bài tập/quiz mới được giao, hoặc lúc sinh viên rà kế hoạch học trong tuần. Đây là trigger ngoài đời; notification chỉ có thể nhắc lại. |
| Effort | Vài phút đến vài giờ tùy nhiệm vụ; cần thời gian học thực tế chứ không chỉ thao tác trên app. |
| Value timing | Giá trị tích lũy: giá trị rõ nhất khi nhiệm vụ hoàn thành trước hạn và sinh viên thấy tiến độ tuần. |
| State | Task, deadline, mức ưu tiên, lịch đã lập, trạng thái hoàn thành và lịch sử hoàn thành được lưu lại. |
| Dependency | Phụ thuộc lịch học, thời điểm giảng viên giao bài, deadline và năng lực/thời gian của sinh viên. |
| Repeat condition | Mỗi tuần học có bài tập, buổi ôn hoặc deadline mới cần được ưu tiên và hoàn thành. |

- **Dạng hành vi:** tiến trình tích lũy theo chu kỳ học tập.
- **Kết luận cadence:** Đối với sinh viên đại học tự quản lý deadline, core action hoàn thành nhiệm vụ học tập đã được lập kế hoạch thường xuất hiện nhiều lần trong **một tuần học** vì bài tập, quiz và deadline được giao theo lịch môn học. Do đó, nhịp đo phù hợp là **theo tuần học** ở cấp **mỗi sinh viên**.

Frequency cao mỗi ngày không tự động tốt hơn: có ngày không có task cần làm, và hoàn thành nhanh ngoài app vẫn là kết quả tốt.

## 03 — Metric System

### Activation

| Thành phần | Định nghĩa |
| --- | --- |
| Start event | `account_created` — sinh viên tạo tài khoản. |
| Activation event | `planned_task_completed_on_time` — sinh viên hoàn thành đúng hạn nhiệm vụ đã nằm trong kế hoạch AI được xác nhận. |
| Time window | Trong 7 ngày kể từ `account_created`. |

Một sinh viên chỉ được xem là activated khi đã nhận giá trị đầu tiên; xem onboarding, đăng nhập hay nhận một kế hoạch AI chưa đủ.

### Engagement

| Góc đo | Metric | Cách đọc |
| --- | --- | --- |
| Frequency | Số `planned_task_completed_on_time` trung vị trên mỗi sinh viên active trong một tuần học | Sinh viên đang nhận value bao nhiêu lần trong cadence tự nhiên. |
| Depth | Tỷ lệ nhiệm vụ trong kế hoạch được hoàn thành đúng hạn trong tuần | Mỗi kế hoạch có dẫn đến tiến độ thực hay không. |

### North Star Metric

**Số sinh viên mỗi tuần hoàn thành ít nhất 2 nhiệm vụ học tập đã được AI lập kế hoạch, đúng hạn.**

- **Unit of value:** sinh viên nhận được tiến độ học tập đúng hạn.
- **Quality threshold:** ít nhất 2 task; mỗi task có trong kế hoạch AI đã xác nhận và hoàn thành không muộn hơn deadline.
- **Frequency:** trong mỗi tuần học (Thứ Hai–Chủ Nhật, timezone của sinh viên).

### Leading indicators

| Leading indicator | Vì sao dự báo core action lặp lại |
| --- | --- |
| Tỷ lệ sinh viên thêm hoặc đồng bộ ít nhất 3 task có deadline trong 48 giờ đầu | Không có đầu việc đáng tin thì AI không thể tạo kế hoạch và không có task để hoàn thành. |
| Tỷ lệ sinh viên xác nhận ít nhất một kế hoạch AI trong 48 giờ sau khi thêm task | Xác nhận kế hoạch tạo trạng thái “task đã được lập kế hoạch”, là tiền đề trực tiếp của core action. |
| Tỷ lệ task trong kế hoạch được bắt đầu trước deadline ít nhất 24 giờ | Bắt đầu đủ sớm làm tăng khả năng hoàn thành đúng hạn; đây là tín hiệu sớm hơn completion. |

### Counter-metric

**Tỷ lệ gợi ý kế hoạch AI bị từ chối hoặc bị sửa lớn** (đổi thứ tự ưu tiên hoặc thời lượng cho từ 50% task trở lên) **không được tăng.**

Nếu NSM tăng vì AI chia task thành các việc quá nhỏ hoặc ép lịch thiếu thực tế, sinh viên sẽ từ chối/sửa nhiều gợi ý. Counter-metric này bảo vệ chất lượng và tính tin cậy của kế hoạch.

## 04 — Retention Definition

| Thành phần | Định nghĩa |
| --- | --- |
| Unit | Một sinh viên (`user_id`). |
| Cohort entry | Tuần học mà sinh viên lần đầu ghi `planned_task_completed_on_time` (cũng là activation event). |
| Return event | `planned_task_completed_on_time`. |
| Window | Các tuần học kế tiếp, từ Thứ Hai 00:00 đến Chủ Nhật 23:59 theo timezone đã chọn của sinh viên. |
| Threshold | Ít nhất 2 return events trong mỗi tuần học. |
| Segment | Sinh viên đại học tự đăng ký, đang trong học kỳ hoạt động, đã thêm/đồng bộ ít nhất 3 task có deadline. |

**Cách báo cáo:** Với cohort sinh viên activated trong tuần W0, tỷ lệ retained W1/W2/W3/W4 là tỷ lệ sinh viên đạt ít nhất 2 `planned_task_completed_on_time` ở tuần tương ứng. So sánh trước hết theo chu kỳ một tuần, cùng segment và sau đó mới đối chiếu benchmark sản phẩm học tập tương đương; không dùng D7 rời rạc.

## 05 — Product Loop

- **Loại loop chính:** progress loop theo chu kỳ học tập.

```text
Chu kỳ 1
Deadline/bài tập mới → sinh viên thêm task → AI sắp xếp ưu tiên và lịch
→ sinh viên xác nhận kế hoạch → hoàn thành task đúng hạn
→ thấy tiến độ + hệ thống lưu workload, thời lượng và lịch sử hoàn thành

Chu kỳ 2
Deadline/bài tập mới của tuần tiếp theo → AI dùng lịch sử để đề xuất lịch vừa sức hơn
→ sinh viên xác nhận/chỉnh kế hoạch → hoàn thành task đúng hạn
→ tiến độ đáng tin hơn và dữ liệu kế hoạch phong phú hơn → lặp lại
```

**Reason to return không dựa vào notification:** bài tập và deadline mới trong lịch học tạo nhu cầu tự nhiên; lịch sử workload giúp kế hoạch tuần sau tốt hơn.

**Metric hypothesis:** Nếu progress loop này hoạt động, **W1–W4 weekly retention của sinh viên activated** sẽ tăng trong **4 tuần sau khi triển khai luồng xác nhận kế hoạch và dùng lịch sử workload**, vì mỗi lần hoàn thành task vừa tạo tiến độ hữu hình vừa giúp gợi ý kế hoạch cho deadline kế tiếp phù hợp hơn.

## 06 — Tracking nhanh

| Tên event | Ý nghĩa | Thời điểm ghi nhận | Metric sử dụng |
| --- | --- | --- | --- |
| `account_created` | Sinh viên đã tạo tài khoản. | Sau khi tài khoản được tạo thành công ở backend. | Activation start event; mẫu số activation. |
| `study_task_added` | Một task học tập có deadline được tạo hoặc đồng bộ thành công. | Khi task được persist thành công, có `task_id` và `due_at`. | Leading indicator: thêm ≥3 task trong 48 giờ; điều kiện segment. |
| `study_plan_generated` | Hệ thống đã tạo một bản kế hoạch AI có task cụ thể. | Khi bản kế hoạch được lưu thành công với `plan_id`; không bắn chỉ vì user bấm nút. | Chẩn đoán funnel từ task sang plan. |
| `study_plan_confirmed` | Sinh viên chấp nhận kế hoạch AI để dùng. | Khi sinh viên lưu/xác nhận kế hoạch; ghi `plan_id`, số task và phiên bản plan. | Leading indicator: xác nhận kế hoạch; precondition cho core action. |
| `planned_task_started` | Sinh viên bắt đầu một task trong kế hoạch. | Khi task lần đầu chuyển từ `not_started` sang `in_progress`. | Leading indicator: bắt đầu ≥24 giờ trước deadline. |
| `planned_task_completed_on_time` | Giá trị lõi: một task trong kế hoạch đã hoàn thành đúng hạn. | Khi task chuyển từ chưa hoàn thành sang hoàn thành và `completed_at <= due_at`. | Activation, engagement frequency/depth, NSM, cohort entry, retention, return event. |
| `study_plan_suggestion_rejected` | Sinh viên từ chối toàn bộ gợi ý kế hoạch AI. | Khi sinh viên chọn “từ chối” và hệ thống lưu quyết định cho `plan_id`. | Counter-metric: tỷ lệ gợi ý bị từ chối. |
| `study_plan_materially_edited` | Sinh viên sửa lớn gợi ý AI. | Khi lưu plan và thay đổi thứ tự ưu tiên hoặc thời lượng của ≥50% task so với plan được tạo. | Counter-metric: tỷ lệ gợi ý bị sửa lớn. |

### Acceptance criteria

1. Với mỗi cặp `user_id` và `task_id`, hệ thống chỉ ghi `planned_task_completed_on_time` khi task chuyển từ trạng thái chưa hoàn thành sang hoàn thành, task thuộc một `plan_id` đã được xác nhận, và `completed_at <= due_at`. Reload trang, retry API hoặc autosave không được tạo event thứ hai cho cùng lần chuyển trạng thái.
2. `study_plan_confirmed` chỉ được gửi sau khi backend persist một plan có `plan_id` và ít nhất một task. Bấm “xác nhận” rồi lỗi mạng, đóng modal hoặc chỉ xem preview không được tính là confirmed.
3. `study_plan_materially_edited` chỉ được gửi một lần cho mỗi cặp `user_id` + `plan_id`; mức sửa lớn phải được tính từ diff server-side giữa phiên bản AI tạo và phiên bản sinh viên lưu, không suy ra từ click trên giao diện.

## Revision note

Không có dự án cụ thể trong workspace ban đầu, nên chọn use case mẫu “AI Personal Assistant for Students” mà brief cho phép. Khi có mô tả dự án thật, cần thay toàn bộ chuỗi quyết định từ core job, không chỉ đổi tên dự án.
