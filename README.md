**Họ tên:** Nguyễn Văn Thăng · **Dự án:** AI Agent hỗ trợ nhân viên CSKH xử lý khiếu nại

# 00 — Phạm vi

- **1. Dự án:** AI Agent hỗ trợ nhân viên CSKH xử lý khiếu nại trong dịch vụ gọi xe.

- **2. Persona:** Nhân viên Chăm sóc khách hàng (CSKH) phụ trách tiếp nhận và xử lý các case khiếu nại.

- **3. Core job:** *“Tôi cần nhanh chóng xác minh một khiếu nại bằng cách thu thập, tra cứu và đối chiếu thông tin từ khách hàng, chuyến đi, tài xế và các bằng chứng liên quan, để xác định case còn thiếu hay mâu thuẫn thông tin gì và đưa ra bước xử lý tiếp theo.”*

---

# 01 — Core Action

## 1. Phân biệt bốn khái niệm

| **Khái niệm** | **Câu trả lời** |
| :--- | :--- |
| **Core job** | Xác minh một khiếu nại bằng cách thu thập, tra cứu và đối chiếu các thông tin liên quan để xác định case còn thiếu hoặc mâu thuẫn thông tin gì và đưa ra bước xử lý tiếp theo. |
| **Core action** | Nhân viên CSKH **review và hoàn tất xác minh một case khiếu nại** dựa trên thông tin đã được tổng hợp và đối chiếu. |
| **Core value** | Nhân viên CSKH có đủ thông tin đáng tin cậy để hiểu tình trạng của case và xác định bước xử lý tiếp theo, đồng thời giảm công việc tra cứu và tổng hợp thủ công. |
| **Core value event** | `case_verification_completed` |

> **Lựa chọn Core Action:** “Nhân viên CSKH hoàn tất xác minh một case khiếu nại.”

Core action không phải là **“AI phân tích case”** hay **“AI tạo recommendation”**, vì đó chỉ là output của hệ thống. Giá trị chỉ được tiến gần rõ rệt khi nhân viên CSKH thực sự review thông tin và hoàn thành bước xác minh case.

---

## 2. Core Action Card

| **Thành phần** | **Câu trả lời của bạn** |
| :--- | :--- |
| **Target user** | Nhân viên CSKH phụ trách xử lý khiếu nại. |
| **Core job** | Xác minh một khiếu nại bằng cách thu thập, tra cứu và đối chiếu thông tin để xác định tình trạng case và bước xử lý tiếp theo. |
| **Core action** | Nhân viên CSKH **review và hoàn tất xác minh một case khiếu nại**. |
| **Object** | Một **case khiếu nại** đang được nhân viên CSKH xử lý. |
| **Preconditions** | Case đã được tiếp nhận; có thông tin khiếu nại cơ bản và các dữ liệu liên quan có thể truy xuất như thông tin chuyến đi, khách hàng, tài xế, giải trình hoặc bằng chứng nếu có. |
| **Completion rule** | Action hoàn tất khi nhân viên CSKH đã review thông tin của case, xác nhận/chỉnh sửa kết quả tổng hợp và chuyển case khỏi bước xác minh sang một bước xử lý tiếp theo. |
| **Core value** | Nhân viên CSKH có được bức tranh tổng hợp và đáng tin cậy về case để tiếp tục xử lý mà không phải tự tra cứu, tổng hợp và đối chiếu toàn bộ thông tin một cách thủ công. |
| **Evidence of value** | Case hoàn tất bước xác minh và được nhân viên chuyển sang bước xử lý tiếp theo dựa trên thông tin đã review. |
| **Candidate event** | `case_verification_completed` |

---

## 3. Tự kiểm Core Action

| **Tiêu chí** | **Đạt?** | **Giải thích** |
| :--- | :---: | :--- |
| **1. Gần core value** | ✅ | Hoàn tất xác minh nghĩa là nhân viên đã có đủ context cần thiết để tiếp tục xử lý case. |
| **2. Có thể lặp lại** | ✅ | Hành vi này được lặp lại mỗi khi nhân viên CSKH xử lý một case khiếu nại mới. |
| **3. Có thể quan sát** | ✅ | Có thể xác định chính xác thời điểm case rời bước xác minh và chuyển sang bước tiếp theo. |
| **4. Có ý nghĩa** | ✅ | Nếu nhiều case được xác minh thành công với ít thao tác thủ công hơn, sản phẩm đang hỗ trợ đúng công việc chính của CSKH. |
| **5. Có thể tác động** | ✅ | Team có thể cải thiện khả năng hoàn tất xác minh bằng cách nâng chất lượng tổng hợp thông tin, phát hiện thiếu/mâu thuẫn, tra cứu chuyến và UX review. |

**Kết quả: 5/5 tiêu chí đạt → Core Action đứng vững.**

---

## 4. Vì sao không chọn các hành vi khác?

Không chọn **`login`**, **`app_opened`** hay **“mở case”** vì đây chỉ là các thao tác để bắt đầu sử dụng hệ thống, chưa chứng minh nhân viên nhận được giá trị.

Không chọn **“hỏi AI”** vì số lần hỏi AI nhiều hơn không đồng nghĩa sản phẩm tốt hơn. Ngược lại, nhân viên phải hỏi AI quá nhiều lần có thể cho thấy hệ thống chưa cung cấp đủ context.

Không chọn **“AI hoàn thành phân tích”** vì đây là output của hệ thống, không phải hành vi của người dùng. AI có thể sinh kết quả nhưng nhân viên CSKH chưa đọc, chưa tin tưởng hoặc không sử dụng kết quả đó.

Vì vậy, hành vi **“Nhân viên CSKH review và hoàn tất xác minh một case khiếu nại”** được chọn làm Core Action vì nó có **actor rõ ràng (CSKH)**, **object rõ ràng (case khiếu nại)** và **completion rule rõ ràng (case hoàn tất bước xác minh và được chuyển sang bước xử lý tiếp theo)**.

---

# 02 — Nature & cadence

## 1. Action Nature Card

Core Action đã chọn:

> **Nhân viên CSKH review và hoàn tất xác minh một case khiếu nại.**

| **Thành phần** | **Câu trả lời** |
| :--- | :--- |
| **Actor** | Nhân viên CSKH phụ trách xử lý case khiếu nại. |
| **Intent** | Nhân viên cần xác minh đủ thông tin của một case để hiểu tình trạng khiếu nại và xác định bước xử lý tiếp theo. |
| **Trigger** | Chủ yếu là **sự kiện bên ngoài**: một case khiếu nại mới được tiếp nhận và được đưa vào hàng đợi/phân công cho nhân viên CSKH. Action cũng có thể tiếp tục khi có thêm thông tin từ khách hàng hoặc tài xế. |
| **Effort** | Mức effort trung bình đến cao. Nhân viên phải review nội dung khiếu nại, thông tin chuyến đi, thông tin khách hàng/tài xế, giải trình và bằng chứng nếu có; đồng thời kiểm tra các thông tin thiếu hoặc mâu thuẫn. Thời gian phụ thuộc độ phức tạp của từng case. |
| **Value timing** | Value xuất hiện chủ yếu **sau khi hoàn tất xác minh một case**. Với case thiếu thông tin hoặc cần giải trình, value có thể bị trì hoãn do phụ thuộc phản hồi của bên khác. |
| **State** | Sau action, case lưu lại kết quả xác minh, thông tin đã được nhân viên xác nhận/chỉnh sửa, các điểm thiếu hoặc mâu thuẫn, trạng thái mới và bước xử lý tiếp theo. |
| **Dependency** | Phụ thuộc vào dữ liệu chuyến đi, thông tin khách hàng, tài xế, bằng chứng và trong một số case là phản hồi/giải trình của tài xế hoặc thông tin bổ sung từ khách hàng. |
| **Repeat condition** | Action xuất hiện lại khi nhân viên được giao **một case mới**, hoặc khi case hiện tại nhận thêm thông tin cần review và xác minh tiếp. |

---

## 2. Dạng hành vi

**Dạng hành vi được chọn: `Workflow của team` kết hợp `phản ứng theo sự kiện`.**

Core Action không phải một thói quen mà nhân viên chủ động thực hiện để duy trì engagement với sản phẩm. Nó xuất hiện vì **công việc thực tế tạo ra nhu cầu xử lý**.

Luồng tự nhiên có thể được mô tả:

```text
Khiếu nại phát sinh
        ↓
Case được tiếp nhận
        ↓
Case được phân công cho CSKH
        ↓
CSKH review thông tin
        ↓
Xác minh / yêu cầu bổ sung thông tin
        ↓
Hoàn tất xác minh
        ↓
Chuyển sang bước xử lý tiếp theo
```

Do đó, số lần Core Action xuất hiện phụ thuộc chủ yếu vào **số case cần xử lý**, không phải số lần nhân viên mở ứng dụng.

---

## 3. Kết luận cadence

> **Đối với nhân viên CSKH xử lý khiếu nại, core action “review và hoàn tất xác minh một case khiếu nại” thường xuất hiện mỗi khi có một case được phân công và đủ điều kiện để xác minh, vì đây là workflow được kích hoạt bởi khiếu nại thực tế chứ không phải thói quen sử dụng sản phẩm. Do đó, nhịp đo phù hợp là theo từng case và tổng hợp theo ca/ngày làm việc ở cấp nhân viên CSKH.**

### Cadence chính

**Đơn vị tự nhiên nhất: `per case`.**

Mỗi case là một cơ hội độc lập để Core Action xảy ra:

```text
1 case đủ điều kiện xác minh
        ↓
1 cơ hội thực hiện Core Action
        ↓
case_verification_completed
```

Có thể tổng hợp các kết quả theo **ca hoặc ngày làm việc** để theo dõi hiệu quả vận hành, nhưng không coi việc nhân viên quay lại mỗi ngày là bằng chứng trực tiếp của product value.

---

## 4. Frequency cao hơn có luôn tốt hơn không?

**Không.**

Ví dụ:

```text
Nhân viên A
10 case → 9 case hoàn tất xác minh

Nhân viên B
30 lần tương tác với AI → 5 case hoàn tất xác minh
```

Không thể kết luận nhân viên B nhận được nhiều value hơn chỉ vì tương tác với AI nhiều hơn.

Trong sản phẩm này, các chỉ số như:

- số lần hỏi AI;
- số lần mở case;
- thời gian sử dụng hệ thống;
- số lần AI được gọi;

tăng lên **không nhất thiết là tín hiệu tốt**.

Ngược lại, nếu nhân viên có thể hoàn tất xác minh một case với **ít thao tác hơn, ít tra cứu thủ công hơn và thời gian ngắn hơn** nhưng vẫn đảm bảo chất lượng, đó có thể là tín hiệu sản phẩm tạo ra nhiều value hơn.

---

## 5. Nature vs Nurture

### Nature

Nhu cầu tự nhiên xuất phát từ:

> **Có case khiếu nại cần được nhân viên CSKH xác minh.**

Không có case thì không có lý do tự nhiên để nhân viên thực hiện Core Action.

### Nurture

Sản phẩm có thể hỗ trợ workflow bằng các cơ chế như:

- ưu tiên case cần xử lý;
- thông báo khi case có thông tin mới;
- nhắc case sắp vượt SLA;
- đưa các thông tin liên quan vào cùng một context;
- chỉ ra thông tin còn thiếu hoặc mâu thuẫn.

Tuy nhiên, các cơ chế này chỉ giúp nhân viên **xử lý nhu cầu đã tồn tại**, không được tạo ra một nhịp sử dụng giả.

```text
Nature:
Case cần xử lý
      ↓
Nhu cầu xác minh
      ↓
Core Action

Nurture:
Giảm friction + đưa đúng thông tin
      ↓
Core Action dễ hoàn thành hơn
```

---

# 03 — Metric System

## 0. Quy tắc đo chung

**Case đủ điều kiện xác minh** là case đã được phân công cho một CSKH đang trong ca làm việc, chưa hoàn tất xác minh lần đầu, không bị hủy/đánh dấu trùng, và có dữ liệu tối thiểu để review: nội dung khiếu nại, mã chuyến đi, thông tin khách hàng/tài xế cùng các nguồn dữ liệu bắt buộc theo loại khiếu nại có thể truy xuất. Không yêu cầu AI đã tổng hợp thành công mới được tính đủ điều kiện, để vẫn đo được trường hợp hệ thống chưa chuẩn bị context.

`is_verification_eligible` lưu khả năng xử lý theo dữ liệu/trạng thái nghiệp vụ của case. Một **cơ hội thực tế** chỉ được tính khi khả năng này là `true`, case đã được giao và CSKH phụ trách đang trong ca; vì vậy case sẵn sàng ngoài ca chỉ bắt đầu tạo cơ hội khi ca làm việc bắt đầu.

- Case đang chờ **phản hồi/bằng chứng bắt buộc** để tiếp tục xác minh có `is_verification_eligible = false` và `eligibility_reason = waiting_required_response`. Khi thông tin bắt buộc được bổ sung và CSKH có thể tiếp tục review, trạng thái chuyển thành `true`.
- Việc phát hiện thiếu thông tin không bắt buộc hoặc một mâu thuẫn cần review không tự động loại case khỏi mẫu số. CSKH phải ghi nhận và xác định hướng xử lý cho các điểm này.
- Kỳ đo `T` có thời điểm bắt đầu và kết thúc rõ ràng: một ca cho báo cáo cá nhân, một ngày hoặc tuần cho báo cáo team; dùng múi giờ `Asia/Bangkok` và khoảng `[start_at, end_at)`.
- Tập `S_T` gồm các `case_id` duy nhất có ít nhất một thời điểm đủ điều kiện trong `T`, bao gồm case tồn từ kỳ trước chưa hoàn tất lần đầu. Case chỉ chờ phản hồi trong toàn bộ `T` không thuộc `S_T`. Case đã đủ điều kiện rồi mới chuyển sang chờ vẫn thuộc `S_T`, tránh làm mẫu số giảm khi gặp case khó.
- Completion Rate và QVCR chỉ lấy kết quả **hoàn tất xác minh lần đầu trong T** của case thuộc `S_T`. Case chưa hoàn tất tiếp tục được xét ở kỳ sau nếu có cơ hội xử lý; báo cáo theo kỳ không cộng các mẫu số để suy ra số case duy nhất toàn thời gian.
- Mỗi case được đếm tối đa một lần trong tử số và mẫu số của từng metric theo kỳ. Case reopen được theo dõi bằng Rework Rate; các lần hoàn tất lại không làm tăng Completion Rate hoặc QVCR. Ở cấp cá nhân, cơ hội được gắn với CSKH đang phụ trách tại thời điểm đủ điều kiện; kết quả chỉ tính cho CSKH thực sự hoàn tất case. Ở cấp team luôn loại trùng theo `case_id`.
- Mẫu số bằng 0 được báo cáo là **N/A — không có cơ hội quan sát**, không quy thành 0%.

## 1. Activation Metric

Activation cần chứng minh nhân viên CSKH đã **chạm core value lần đầu**, không chỉ đăng nhập hoặc mở một case.

| **Thành phần** | **Định nghĩa** |
| :--- | :--- |
| **Start event** | `first_eligible_case_assigned` — mốc suy ra khi CSKH lần đầu có case được giao và đủ điều kiện trong ca, từ `case_assigned`, `case_eligibility_changed` kết hợp lịch ca. Đây là mốc phân tích, không phải event phát thêm. |
| **Activation event** | `case_verification_completed` — nhân viên review, xác nhận/chỉnh sửa thông tin và hoàn tất xác minh case đầu tiên. |
| **Time window** | Từ mốc đầu tiên có case đủ điều kiện đến hết chính ca đó. Nếu case được giao khi đang chờ phản hồi bắt buộc, window chỉ bắt đầu khi case đủ điều kiện trong một ca làm việc. |

### Activation Metric

> **Tỷ lệ nhân viên CSKH hoàn tất xác minh lần đầu ít nhất 1 case trong ca đầu tiên có case được giao và đủ điều kiện xử lý.**

Công thức:

```text
Activation Rate =
Số CSKH duy nhất hoàn tất lần đầu ≥ 1 case đủ điều kiện trong ca đầu tiên
-------------------------------------------------------------
Số CSKH duy nhất có ca đầu tiên được giao case đủ điều kiện đã kết thúc
× 100%
```

Tử số chỉ lấy CSKH thuộc mẫu số; ca chưa kết thúc chưa vào báo cáo activation chính thức.

Không sử dụng `login`, `app_opened` hoặc hoàn thành onboarding làm activation vì các event này chưa chứng minh nhân viên đã nhận được core value.

---

## 2. Engagement Metrics

Vì cadence tự nhiên là **per case**, chọn hai góc đo là **frequency** và **depth**.

### Metric 1 — Frequency: Verification Completion Rate

Đo tỷ lệ các cơ hội thực hiện Core Action thực sự được hoàn tất trong kỳ `T`.

```text
Verification Completion Rate =
COUNT(DISTINCT case_id thuộc S_T hoàn tất xác minh lần đầu trong T)
----------------------------------------------------------------
COUNT(DISTINCT case_id thuộc S_T)
× 100%
```

Metric này phù hợp hơn số lần sử dụng AI vì nó gắn trực tiếp với workflow thực tế.

Ví dụ: `S_T` có 10 case, 8 case hoàn tất lần đầu; một case trong số đó reopen rồi hoàn tất lại. Dù có 9 completion events, Completion Rate vẫn là **8/10 = 80%**.

### Metric 2 — Depth: Full Review Rate

```text
Full Review Rate =
Số case duy nhất trong R_T có toàn bộ hạng mục review bắt buộc được CSKH xác nhận
-----------------------------------------------------------------------------
Số case duy nhất trong R_T
× 100%
```

`R_T` gồm các case được CSKH bắt đầu review lần đầu trong `T`. Checklist được chụp tại thời điểm hoàn tất lần đầu, hoặc cuối kỳ nếu chưa hoàn tất. Case chưa review đủ vẫn ở mẫu số. Checklist phụ thuộc loại khiếu nại, gồm review nội dung khiếu nại, đối chiếu chuyến đi, thông tin các bên, bằng chứng bắt buộc, ghi nhận thiếu/mâu thuẫn và bước xử lý tiếp theo. Mục không áp dụng cần có lý do do CSKH xác nhận; việc AI tự đánh dấu không được tính là đã review.

Metric này đo **mức độ review đầy đủ**, không đo số thao tác hoặc thời gian ở trên màn hình. Nó khác QVCR: Full Review Rate xét các case bắt đầu review, còn QVCR xét kết quả hoàn tất đạt chuẩn trên toàn bộ cơ hội đủ điều kiện.

### Chỉ số hiệu quả xử lý — Median Verification Time

```text
Median Verification Time =
Median(
    verification_completed_at
    -
    verification_started_at
)
```

Đo thời gian nhân viên cần để đi từ bắt đầu review đến hoàn tất xác minh một case.

Chỉ lấy lần xác minh đầu tiên của các case hoàn tất trong `T`, ghép start và completion theo `verification_cycle_id`. Đây là thời gian trôi qua, có thể gồm thời gian chờ phản hồi; cần phân nhóm theo loại/độ phức tạp case và có/không chờ phản hồi trước khi so sánh. Không gọi chỉ số này là depth hoặc thời gian thao tác thực tế của CSKH.

Một vòng xác minh giữ nguyên `verification_cycle_id` khi tạm chờ rồi tiếp tục hoặc bàn giao CSKH; thời điểm start là lần bắt đầu sớm nhất của vòng đó. Chỉ tạo vòng mới khi reopen sau completion.

Thời gian giảm có thể cho thấy AI giúp giảm công việc tra cứu, tổng hợp và đối chiếu thủ công. Tuy nhiên, metric này phải được đọc cùng **quality threshold** để tránh tối ưu tốc độ bằng cách xác minh case qua loa.

---

## 3. North Star Metric

### North Star Metric được chọn

> **Số case khiếu nại được CSKH hoàn tất xác minh đạt quality threshold trên mỗi 100 case đủ điều kiện xác minh.**

Có thể gọi metric:

**Quality-Verified Case Rate (QVCR)**

```text
QVCR =
COUNT(DISTINCT case_id thuộc S_T hoàn tất lần đầu trong T và đạt quality threshold)
--------------------------------------------------------------------------------
COUNT(DISTINCT case_id thuộc S_T)
× 100
```

### Ba thành phần của NSM

| **Thành phần** | **Định nghĩa** |
| :--- | :--- |
| **Unit of value** | Một case khiếu nại được hoàn tất xác minh. |
| **Quality threshold** | Case có đủ các trường thông tin bắt buộc cho loại khiếu nại; checklist review bắt buộc được CSKH xác nhận đầy đủ; các thông tin thiếu/mâu thuẫn quan trọng được ghi nhận kèm hướng xử lý; và kết quả/bước tiếp theo được CSKH xác nhận trước khi chuyển bước. Kiểm tra trên snapshot của lần hoàn tất đầu tiên. |
| **Frequency** | Số case duy nhất hoàn tất lần đầu đạt chuẩn trong `T` trên mỗi **100 case thuộc S_T**. |

### Vì sao chọn NSM này?

NSM không đo số lần nhân viên hỏi AI mà đo **kết quả công việc có giá trị** mà nhân viên đạt được với sản phẩm.

Việc dùng mẫu số là số case đủ điều kiện cũng hạn chế vấn đề:

```text
Tuần A: có 1.000 case đủ điều kiện → hoàn tất lần đầu đạt chuẩn 800
Tuần B: có   500 case đủ điều kiện → hoàn tất lần đầu đạt chuẩn 450
```

Nếu chỉ nhìn số lượng tuyệt đối thì tuần A có vẻ tốt hơn.

Nhưng:

```text
A = 80 case đạt chuẩn / 100 case
B = 90 case đạt chuẩn / 100 case
```

Tuần B thực tế có hiệu quả xác minh tốt hơn.

---

## 4. Leading Indicators

Chọn tối đa ba leading indicators:

| **Leading indicator** | **Vì sao tin nó dự báo Core Action lặp lại?** |
| :--- | :--- |
| **Context Ready Rate** — tỷ lệ case mà thông tin chuyến, khách hàng, tài xế và evidence liên quan được hệ thống tổng hợp thành công trước khi review. | Nếu context cần thiết có sẵn, nhân viên phải tra cứu thủ công ít hơn và có khả năng hoàn tất xác minh cao hơn. |
| **AI Analysis Acceptance Rate** — tỷ lệ phân tích AI được nhân viên chấp nhận hoặc chỉ chỉnh sửa nhỏ trước khi tiếp tục workflow. | Nếu kết quả AI đủ hữu ích để sử dụng, nhân viên có nhiều khả năng tiếp tục dựa vào hệ thống ở các case tiếp theo. |
| **Median Verification Time của kỳ trước** | Dùng như giả thuyết dự báo việc lặp lại Core Action trong ca đủ điều kiện tiếp theo, khi kiểm soát độ khó case và chất lượng. Đây là kết quả của case đã hoàn tất, không phải leading indicator cho chính completion đó. |

**Cách tính:** Context Ready Rate = số case duy nhất trong `R_T` có `context_ready_at` không muộn hơn thời điểm bắt đầu review / số case trong `R_T`. AI Analysis Acceptance Rate = số kết quả review cuối cùng có `review_outcome` là `accepted` hoặc `minor_edit` / số `analysis_id` duy nhất được CSKH review trong `T`. Các mối quan hệ dự báo trên là giả thuyết cần kiểm chứng bằng dữ liệu.

---

## 5. Counter-metrics

Core Action tăng không được đánh đổi bằng chất lượng xác minh.

### Counter-metric chính — Rework Rate

```text
Rework Rate =
Số case duy nhất trong C_T reopen trong 7 ngày sau lần hoàn tất đầu tiên
---------------------------------------------------------------------
Số case duy nhất trong C_T
× 100%
```

`C_T` là tập case hoàn tất lần đầu trong `T` và đã có đủ 7 ngày theo dõi. Case chưa đủ thời gian theo dõi được báo cáo là chưa đủ dữ liệu; nhiều lần reopen của cùng case chỉ tính một lần.

Nếu `case_verification_completed` tăng mạnh nhưng `Rework Rate` cũng tăng, có thể nhân viên đang hoàn tất case quá nhanh hoặc AI cung cấp kết quả chưa đủ chính xác.

### Counter-metric bổ sung — Major AI Correction Rate

```text
Major AI Correction Rate =
Số AI analysis bị CSKH sửa đáng kể hoặc loại bỏ
------------------------------------------------
Số AI analysis được CSKH review
× 100%
```

Metric này giúp phát hiện trường hợp hệ thống vẫn tạo nhiều output nhưng output không đủ tin cậy để nhân viên sử dụng.

Mỗi `analysis_id` chỉ tính một lần theo kết quả review cuối cùng trong `T`; `major_edit` và `rejected` vào tử số. Tử số và mẫu số dùng cùng tập kết quả review như AI Analysis Acceptance Rate.

---

# 04 — Retention Definition

## 1. Retention Definition

Retention trong sản phẩm này không nên được hiểu là:

> “Nhân viên có đăng nhập lại vào ngày hôm sau hay không?”

Nhân viên CSKH có thể đăng nhập vì yêu cầu công việc dù sản phẩm không tạo ra nhiều value.

Retention cần gắn với việc **Core Action được thực hiện lại trên các case tiếp theo**.

| **Thành phần** | **Định nghĩa** |
| :--- | :--- |
| **Unit** | Nhân viên CSKH. |
| **Cohort entry** | `case_verification_completed` đầu tiên — nhân viên đã hoàn tất xác minh case đầu tiên và chạm core value. |
| **Return event** | `case_verification_completed` trên **một case khác**. |
| **Window** | **Ca đủ điều kiện thứ k sau ca activation**, với `k = 1, 2, 3`; chỉ số chính là `k = 1`. Không tính phần còn lại của ca activation là một ca quay lại. |
| **Threshold** | Hoàn tất xác minh lần đầu ít nhất **1 case khác với case activation**, thuộc tập cơ hội đủ điều kiện của CSKH trong chính ca thứ k. Hoàn tất lại case reopen không tính là return event. |
| **Segment** | CSKH trực tiếp xử lý khiếu nại, đã activation và có ca đủ điều kiện thứ k đã kết thúc tại thời điểm chốt báo cáo; so sánh riêng theo team/loại khiếu nại. |

---

## 2. Retention Metric

> **Eligible-Shift Core Action Retention**

Sau ca activation, đánh số riêng cho từng CSKH các ca có ít nhất một case được giao, chưa hoàn tất lần đầu và đủ điều kiện để xử lý. Ca nghỉ hoặc ca không có cơ hội không tăng `k`; case tồn chưa hoàn tất có thể tạo cơ hội ở ca tiếp theo.

```text
Retention(k) =
Số CSKH duy nhất hoàn tất lần đầu ≥ 1 case khác trong ca đủ điều kiện thứ k
------------------------------------------------------------------------
Số CSKH duy nhất trong cohort có ca đủ điều kiện thứ k đã kết thúc
× 100%
```

Cohort được nhóm theo tuần có completion đầu tiên. Báo cáo `Retention(1)` là chỉ số chính và `Retention(2)`, `Retention(3)` để theo dõi các cơ hội tiếp theo, kèm mẫu số từng mốc. CSKH chưa có ca thứ k hoặc ca đó chưa kết thúc được ghi là chưa đủ dữ liệu. Không hoàn tất ở một ca đủ điều kiện là không retained tại mốc đó, chưa đủ để kết luận nhân viên đã churn vĩnh viễn.

Tử số chỉ lấy CSKH thuộc mẫu số của cùng cohort và cùng mốc `k`.

Một nhân viên được xem là retained nếu:

```text
Đã hoàn tất case đầu tiên
        ↓
Có ca đủ điều kiện thứ k sau ca activation đã kết thúc
        ↓
Trong ca có ≥ 1 case đủ điều kiện xác minh
        ↓
Hoàn tất lần đầu ≥ 1 case khác với case activation trong ca đó
        ↓
RETAINED
```

Ngược lại:

```text
Không có case đủ điều kiện trong ca
        ↓
KHÔNG tính là churn
```

Điểm này quan trọng vì Core Action phụ thuộc vào nguồn case. Không thể kết luận nhân viên không retained khi họ không có cơ hội thực hiện hành vi.

---

## 3. Vì sao không dùng D1/D7 Retention đơn thuần?

Core Action của sản phẩm có nature là:

**workflow của team + phản ứng theo sự kiện.**

Vì vậy:

```text
D7 login retention
```

không trực tiếp chứng minh sản phẩm tạo value.

Ví dụ một nhân viên nghỉ cuối tuần hoặc không được giao case thì không thực hiện Core Action là điều bình thường.

Do đó retention phải được tính trên **các window mà nhân viên thực sự có cơ hội xử lý case**.

---

## 4. So sánh retention với ba mốc

### Natural cycle

So với chu kỳ tự nhiên của công việc: các **ca làm việc có case đủ điều kiện xử lý**.

### Cohort đúng segment

So sánh giữa các nhóm nhân viên tương đồng, ví dụ cùng nhóm xử lý khiếu nại hoặc cùng loại case, thay vì trộn tất cả nhân viên CSKH.

### Benchmark category

Nếu sử dụng benchmark bên ngoài, cần ưu tiên benchmark của các sản phẩm **B2B workflow / customer-support tools** có hành vi tương tự, thay vì benchmark của social app hoặc consumer app.

Không đặt một con số retention cố định trước khi có dữ liệu baseline thực tế.

---

# Tổng hợp Metric System

| **Metric** | **Định nghĩa chính** |
| :--- | :--- |
| **Core Action** | CSKH review và hoàn tất xác minh một case. |
| **Core Value Event** | `case_verification_completed` |
| **Activation** | Hoàn tất lần đầu ≥ 1 case trong ca đầu tiên có case được giao và đủ điều kiện. |
| **Engagement — Frequency** | Verification Completion Rate. |
| **Engagement — Depth** | Full Review Rate — tỷ lệ case bắt đầu review trong kỳ được CSKH review đủ checklist bắt buộc. |
| **Hiệu quả xử lý** | Median Verification Time của lần xác minh đầu tiên. |
| **North Star Metric** | Quality-Verified Case Rate — số case hoàn tất xác minh đạt chuẩn / 100 case đủ điều kiện. |
| **Leading #1** | Context Ready Rate. |
| **Leading #2** | AI Analysis Acceptance Rate. |
| **Leading #3** | Median Verification Time kỳ trước, dự báo giả thuyết cho ca tiếp theo. |
| **Counter-metric** | Rework Rate trong 7 ngày sau completion đầu tiên. |
| **Retention** | Retention(1), bổ sung Retention(2)/(3): hoàn tất lần đầu ≥ 1 case khác trong ca đủ điều kiện thứ k sau ca activation. |

---

# 05 — Product Loop

## 1. Loại loop chính

**Loại loop:** `Workflow loop` kết hợp `Event-response`.

Loop được kích hoạt bởi nhu cầu thực tế trong công việc: **một case khiếu nại cần được xác minh**.

Reason to return không phải notification, streak hay reward. Nhân viên quay lại vì có **case mới hoặc case hiện tại có thêm thông tin cần xử lý**.

---

## 2. Product Loop — hai chu kỳ

```text
CHU KỲ 1

Natural Trigger
Case khiếu nại được phân công cho CSKH
        ↓
Core Action
CSKH review + hoàn tất xác minh case
        ↓
Immediate Value
Có đủ context đáng tin cậy để xác định bước xử lý tiếp theo
        ↓
Saved State / Investment
Lưu kết quả xác minh, chỉnh sửa của CSKH,
thông tin thiếu/mâu thuẫn và trạng thái case
        ↓

────────────────────────────────────────

CHU KỲ 2

Next Natural Trigger
Một case mới được phân công
hoặc case cũ có thêm thông tin cần review
        ↓
Core Action tiếp theo
CSKH tiếp tục review + hoàn tất xác minh
        ↓
Repeat Value
Tiếp tục xử lý case với ít công sức
tra cứu/tổng hợp thủ công hơn
        ↓
Saved State / Investment
Tiếp tục tích lũy lịch sử case,
kết quả review và audit trail
        ↓
Next Natural Trigger
...
```

### Loop rút gọn

```text
Case cần xử lý
      ↓
Context được chuẩn bị
      ↓
CSKH review
      ↓
Hoàn tất xác minh
      ↓
Case chuyển bước
      ↓
Lưu kết quả + lịch sử xử lý
      ↓
Case tiếp theo
      ↓
CSKH tiếp tục hoàn tất xác minh
```

---

## 3. Vì sao loop có lý do lặp lại?

Lý do nhân viên quay lại là:

> **Có case khiếu nại mới cần được xử lý hoặc case hiện tại có thêm thông tin cần xác minh.**

Nếu bỏ toàn bộ notification, nhân viên vẫn có lý do quay lại vì khiếu nại là một phần của workflow công việc.

Notification chỉ có thể hỗ trợ nhân viên biết **khi nào** cần xử lý, chứ không tạo ra nhu cầu xử lý.

---

## 4. Metric Hypothesis

> **Nếu loop này hoạt động, metric Quality-Verified Case Rate (QVCR) sẽ tăng trong 4 tuần thử nghiệm, vì việc chuẩn bị context và lưu trạng thái xử lý giúp nhân viên CSKH giảm công việc tra cứu/tổng hợp thủ công và có thể hoàn tất nhiều case đạt quality threshold hơn trên mỗi 100 case đủ điều kiện xác minh.**

Đồng thời cần kiểm tra `Rework Rate` để đảm bảo QVCR tăng không phải do nhân viên hoàn tất case nhanh nhưng chất lượng xác minh giảm.

---

# 06 — Tracking nhanh

## 1. Core Events

Chỉ tracking các event cần thiết để tính các metric đã xác định ở Phase 3.

| **Tên event** | **Ý nghĩa** | **Thời điểm ghi nhận** | **Metric sử dụng** |
| :--- | :--- | :--- | :--- |
| `case_assigned` | Một case đã được phân công cho CSKH; ghi cả trạng thái đủ điều kiện tại thời điểm giao. | Khi hệ thống xác nhận case đã được gán thành công cho một `agent_id`. | Activation Rate, tập cơ hội S_T, Retention. |
| `case_eligibility_changed` | Case chuyển giữa đủ điều kiện và chưa đủ điều kiện, có lý do cụ thể. | Khi trạng thái nghiệp vụ thực sự thay đổi, ví dụ chờ/nhận phản hồi bắt buộc, hủy hoặc đánh dấu trùng. | Xác định S_T, mốc activation và ca đủ điều kiện cho Retention. |
| `case_verification_started` | CSKH đã thực sự bắt đầu một vòng review/xác minh. | Khi case chuyển từ trạng thái chờ xác minh sang đang xác minh; ghi `verification_cycle_id` và `is_first_verification`. | Full Review Rate, Context Ready Rate, Median Verification Time. |
| `case_context_ready` | Context cần thiết của case đã được hệ thống tổng hợp và sẵn sàng cho CSKH review. | Khi quá trình tổng hợp context hoàn tất thành công và kết quả được hiển thị/sẵn sàng cho CSKH. | Context Ready Rate. |
| `ai_analysis_reviewed` | CSKH đã review kết quả phân tích do AI cung cấp. | Khi CSKH hoàn tất review và xác nhận kết quả là accepted, minor edit hoặc major edit/rejected. | AI Analysis Acceptance Rate, Major AI Correction Rate. |
| `case_verification_completed` | CSKH đã review/xác nhận thông tin và hoàn tất xác minh một case. Đây là **Core Value Event**. | Chỉ ghi khi case thực sự chuyển sang bước xử lý tiếp theo; lưu snapshot checklist và phân biệt lần đầu với hoàn tất lại. | Activation Rate, Verification Completion Rate, Full Review Rate, QVCR, Retention, Median Verification Time. |
| `case_quality_threshold_passed` | Case đã hoàn tất xác minh và đáp ứng các điều kiện chất lượng đã định nghĩa. | Sau khi kiểm tra các trường bắt buộc, thông tin thiếu/mâu thuẫn và xác nhận của CSKH thành công. | Quality-Verified Case Rate (QVCR). |
| `case_verification_reopened` | Một case đã hoàn tất nhưng phải quay lại bước xác minh. | Khi case chuyển từ trạng thái sau xác minh trở lại trạng thái cần xác minh; liên kết với completion trước đó. | Rework Rate. |

**Tổng cộng: 8 core events**, nằm trong giới hạn 4–8 events.

### Thuộc tính và dữ liệu cần lưu

| **Thuộc tính** | **Quy tắc / mục đích** |
| :--- | :--- |
| `event_id`, `event_name` | Bắt buộc trên mọi event; `event_id` duy nhất để loại trùng khi ingest/retry. |
| `case_id` | Bắt buộc trên mọi event; dùng `COUNT(DISTINCT case_id)` cho các metric theo case. |
| `agent_id` | CSKH phụ trách; completion/review phải ghi đúng người thực hiện. Event hệ thống trước khi có người phụ trách có thể để null và không tự tạo cơ hội ở cấp cá nhân. |
| `event_timestamp` | Thời điểm thay đổi nghiệp vụ đã được server xác nhận, lưu UTC; quy đổi sang `Asia/Bangkok` khi chia kỳ. Không dùng thời điểm nhận log làm thời điểm action. |
| `shift_id` | Ca chứa action của CSKH; event hệ thống ngoài ca có thể null. Join lịch ca để xác định cơ hội xử lý trong các ca tiếp theo. |
| `is_verification_eligible`, `eligibility_reason` | Trạng thái đủ điều kiện tại thời điểm event và lý do như `ready`, `waiting_required_response`, `missing_required_data`, `cancelled`, `duplicate`, `already_completed`. Eligibility trong kỳ còn phải đối chiếu người phụ trách và lịch ca. |
| `previous_is_verification_eligible` | Bắt buộc trên `case_eligibility_changed` để tái dựng khoảng đủ/chưa đủ điều kiện; không thay thế lịch sử bằng trạng thái hiện tại. |
| `status_before`, `status_after` | Ghi trên các event chuyển trạng thái để xác nhận start/completion/reopen thật sự xảy ra. |
| `verification_cycle_id`, `is_first_verification` | Ghi trên start, review AI, completion và quality check; ghép đúng một vòng xác minh. Hoàn tất lại sau reopen có `is_first_verification = false`. |
| `analysis_id`, `review_outcome` | Bắt buộc trên `ai_analysis_reviewed`; outcome gồm `accepted`, `minor_edit`, `major_edit`, `rejected`. Lấy kết quả review cuối cùng của mỗi `analysis_id` trong kỳ. |
| `checklist_version`, `required_review_items`, `confirmed_review_items`, `review_complete` | Checklist theo loại khiếu nại và xác nhận thực tế của CSKH, lưu tại completion hoặc snapshot cuối kỳ của case chưa hoàn tất. Mục không áp dụng phải kèm lý do được CSKH xác nhận. |
| `quality_threshold_version`, `quality_passed`, `completion_event_id` | Kết quả kiểm tra chất lượng tại completion; event quality-passed tham chiếu đúng completion và cùng vòng xác minh, tránh dùng kết quả của lần hoàn tất lại cho QVCR lần đầu. |
| `previous_completion_event_id`, `reopen_reason` | Ghi trên reopen để truy về completion trước đó và kiểm tra cửa sổ Rework Rate 7 ngày. |
| `complaint_type`, `complexity_segment` | Nhóm loại/độ khó case, dùng để so sánh thời gian và retention giữa các nhóm tương đồng. |

Ngoài event log, cần **lịch ca đã lưu lịch sử** (`agent_id`, `shift_id`, `start_at`, `end_at`), lịch sử phân công/eligibility, và snapshot checklist của case tại cuối mỗi kỳ. Các snapshot là dữ liệu nghiệp vụ, không thêm event thứ 9. Full Review Rate cần snapshot này để tính cả case bắt đầu review nhưng chưa hoàn tất. `context_ready_at`, `verification_started_at`, `verification_completed_at` được lấy từ timestamp của event tương ứng theo case/vòng xác minh.

Khi mở kỳ báo cáo, lấy trạng thái từ lịch sử trước `start_at`, rồi áp dụng các thay đổi trong kỳ; không chỉ đếm event phát sinh trong `T`, vì case tồn có thể đủ điều kiện mà không phát sinh event phân công mới. Báo cáo cuối kỳ giữ nguyên tập cơ hội đã quan sát, kể cả case sau đó chuyển sang chờ phản hồi.

---

## 2. Mapping Event → Metric

```text
case_assigned
      ↓
Activation Rate
S_T / Verification Completion Rate / QVCR
Retention


case_eligibility_changed + lịch ca / phân công
      ↓
S_T / Verification Completion Rate / QVCR
Activation Rate
Retention


case_verification_started
      ↓
Median Verification Time
Full Review Rate (kết hợp snapshot checklist)
Context Ready Rate (mốc so sánh context sẵn sàng)


case_context_ready
      ↓
Context Ready Rate


ai_analysis_reviewed
      ↓
AI Analysis Acceptance Rate
Major AI Correction Rate


case_verification_completed
      ↓
Activation Rate
Verification Completion Rate
Retention
QVCR
Median Verification Time
Full Review Rate (snapshot tại completion)


case_quality_threshold_passed
      ↓
Quality-Verified Case Rate


case_verification_reopened
      ↓
Rework Rate
```

Như vậy, mỗi event đều phục vụ ít nhất một metric. Không tracking các click như `button_clicked`, `tab_opened` hay `ai_button_clicked` nếu chúng không được sử dụng để tính metric đã xác định.

---

## 3. Acceptance Criteria

### AC-01 — Completion event chỉ ghi khi action thực sự hoàn tất

> Với mỗi cặp `agent_id` và `case_id`, hệ thống chỉ ghi `case_verification_completed` khi case thực sự chuyển từ trạng thái **đang xác minh** sang trạng thái **sau xác minh/bước xử lý tiếp theo**. Việc CSKH bấm nút, mở modal hoặc bắt đầu gửi request nhưng request thất bại không được tạo event này.

### AC-02 — Không ghi trùng event

> Với cùng một lần chuyển trạng thái của `case_id`, hệ thống chỉ ghi một `case_verification_completed`. Reload trang, retry request, autosave hoặc mở lại case không được tạo thêm event cho lần hoàn tất đó.

> Nếu một case reopen và hoàn tất lại, event mới có vòng xác minh mới và `is_first_verification = false`. Với 10 case đủ điều kiện, 8 case hoàn tất lần đầu và 1 lần hoàn tất lại, báo cáo vẫn phải cho Completion Rate = 80%; QVCR cũng không được cộng thêm case đó.

### AC-03 — Reopen phải là một lần chuyển trạng thái thực

> `case_verification_reopened` chỉ được ghi khi một case đã hoàn tất xác minh thực sự chuyển trở lại trạng thái cần xác minh. Việc CSKH chỉ mở lại màn hình chi tiết case để xem thông tin không được tính là reopen.

### AC-04 — Quality threshold phải được kiểm tra sau completion

> `case_quality_threshold_passed` chỉ được ghi khi case đã hoàn tất xác minh và đáp ứng đầy đủ quality threshold đã định nghĩa. Không ghi event chỉ vì AI dự đoán case có đủ thông tin.

> Quality check chạy trên snapshot của completion và tham chiếu `completion_event_id` cùng `verification_cycle_id`. Chỉ snapshot lần đầu được dùng cho QVCR; checklist do AI tự đánh dấu chưa được CSKH xác nhận không đủ để tính Full Review Rate đạt chuẩn.

---

# 07 — Tự soi lỗi & nộp

## 1. Checklist tự soi

| **Câu hỏi kiểm tra** | **Kết quả** | **Giải thích** |
| :--- | :---: | :--- |
| **Core action không phải thao tác giao diện hay output hệ thống?** | ✅ | Core Action là **CSKH review và hoàn tất xác minh một case**, không phải mở app, bấm nút hay AI sinh kết quả. |
| **Activation không phải xem hướng dẫn hay đăng nhập?** | ✅ | Activation chỉ xảy ra khi CSKH hoàn tất lần đầu ít nhất một case trong ca đầu tiên có case được giao và đủ điều kiện. |
| **Frequency không cao hơn nhu cầu thật?** | ✅ | Cadence chính là **per case**. Core Action chỉ có lý do xảy ra khi có case đủ điều kiện xác minh. |
| **Loop có reason to return ngoài notification?** | ✅ | Reason to return là **case mới được phân công hoặc case hiện tại có thêm thông tin cần xử lý**. Notification chỉ hỗ trợ workflow. |
| **Retention không dùng chung một window cho mọi cadence?** | ✅ | Retention được tính ở **ca đủ điều kiện thứ 1, 2, 3 sau ca activation**, với mẫu số chỉ gồm CSKH có ca tương ứng đã kết thúc. |
| **Mọi event đều map về một metric?** | ✅ | 8 core events trong tracking đều được map tới ít nhất một metric ở Phase 3. |
| **Metric nào cũng có event để tính nó?** | ✅ | Mỗi metric có event tương ứng và dữ liệu hỗ trợ được chỉ rõ: lịch ca/phân công, lịch sử eligibility, snapshot checklist. |

**Kết quả: 7/7 tiêu chí đạt.**

---

## 2. Kiểm tra tính nhất quán toàn bài

```text
Core Job
Xác minh khiếu nại để có đủ thông tin cho bước xử lý tiếp theo
        ↓
Core Action
CSKH review và hoàn tất xác minh một case
        ↓
Nature
Workflow + Event-response
        ↓
Natural Cadence
Per case
        ↓
Core Value Event
case_verification_completed
        ↓
North Star Metric
Quality-Verified Case Rate (QVCR)
        ↓
Retention
Hoàn tất lần đầu case khác ở ca đủ điều kiện thứ k
sau ca activation (k = 1, 2, 3)
        ↓
Product Loop
Case → Verify → Value → Saved State → Next Case
        ↓
Tracking
Events trực tiếp phục vụ các metric trên
```

Các quyết định từ Phase 0 đến Phase 4 không mâu thuẫn với nhau.

---

## 3. Revision / Rationale

Sau khi tự kiểm, **không có thay đổi lớn đối với Core Action hoặc cadence**.

Giữ nguyên:

> **Core Action:** “Nhân viên CSKH review và hoàn tất xác minh một case khiếu nại.”

> **Cadence:** `Per case`, tổng hợp theo ca/ngày làm việc khi cần theo dõi vận hành.

**Lý do:** Core Action phản ánh trực tiếp công việc tạo value của nhân viên CSKH, còn cadence `per case` xuất phát từ nature của workflow. Việc ép cadence thành daily/weekly hoặc dùng số lần tương tác với AI sẽ làm metric phụ thuộc vào mức sử dụng hệ thống thay vì giá trị thực tế mà nhân viên nhận được.

Các điểm được chỉnh sau khi rà soát metric và tracking:

- Thay “Depth: Median Verification Time” bằng **Full Review Rate**; giữ thời gian xác minh ở nhóm hiệu quả xử lý và giả thuyết leading cho kỳ sau.
- Định nghĩa case đủ điều kiện, tập `S_T`, kỳ đo và cách xử lý case chờ phản hồi; dùng case duy nhất và kết quả hoàn tất lần đầu để tránh tăng metric do reopen.
- Chốt Retention(1) là chỉ số chính, bổ sung Retention(2)/(3), cùng quy tắc không tính ca chưa có cơ hội hoặc chưa kết thúc.
- Bổ sung event eligibility (tổng 8 events), các thuộc tính bắt buộc và dữ liệu snapshot/lịch ca để có thể tính metric nhất quán.

Nguyên tắc được giữ xuyên suốt:

> **Không có case đủ điều kiện xử lý không được xem là churn**, vì nhân viên không có cơ hội tự nhiên để thực hiện Core Action.

---
