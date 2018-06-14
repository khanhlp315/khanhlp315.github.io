---
layout: single
title:  "Các bài toán về đệ quy và quy hoạch động khi phỏng vấn"
date:   2018-06-15 03:52:56 +0700
categories:
  - Translation
  - Cracking The Coding Interview
---
*Được dịch từ Cracking the Coding Interview, 5th Edition*

Mặc dù có rất nhiều bài toán có thể áp dụng đệ quy, rất nhiều trong số đó đều tuân theo một khuôn mẫu. Cách đơn giản nhất để nhận ra một bài toán có thể áp dụng đệ quy hay không là xem coi vấn đề đó có được xây dựng từ nhiều bài toán nhỏ hay không.

Nếu một bài toán được bắt đầu bằng những câu tương tự như "Thiết kế một giải thuật để tính ... thứ n", "Viết chương trình xuất ra n số đầu tiên...", "Viết một hàm để tìm ra tất cả...", bài toán đó thường là (nhưng không phải lúc nào cũng vậy) một bài toán có thể ứng dụng được đệ quy.

### Cách tiếp cận
Một giải pháp đệ quy sẽ được xây dựng từ những giải pháp nhỏ. Trong đa số trường hợp, điều này có nghĩa là tính f(n) bằng cách thêm, bớt đi hoặc thay đổi cách tính cho f(n-1). Tuy nhiên, trong một số trường hợp khác, chúng ta thường phải làm nhiều thứ phức tạp hơn.
Chúng ta sẽ bắt đầu xem xét tới 2 kiểu đệ quy: đệ quy từ dưới lên và đệ quy từ trên xuống.

* ***Đệ quy từ dưới lên***
 Đệ quy từ dưới lên thường khá dễ thấy. Chúng ta bắt đầu với việc biết cách giải quyết vấn đề cho những trường hợp đơn giản, ví dụ như một mảng chỉ có một phần tử và tìm cách giải quyết cho mảng 2, 3... phần tử. Điểm cốt lõi là tìm ra được cách để xây dựng giải pháp cho một trường hợp từ các trường hợp khác
 * ***Đệ quy từ trên xuống*** 
Đệ quy từ trên xuống thường phức tạp hơn, nhưng nó rất cần thiết cho một số bài toán. Trong những bài toán này, ta tìm cách chia bài toán thành N bài toán nhỏ hơn. Khi sử dụng kiêu đệ quy này, chúng ta cần phải cẩn thận để không khiến nhung trường hợp chồng lên nhau.

### Quy hoạch động
Các bài toán về quy hoạch động thường ít được hỏi trong các buổi phỏng vấn bởi vì nó quá khó cho một buổi phỏng vấn 45 phút. Kể cả những ứng cử viên giỏi cũng thường gặp khó khăn khi giải quyết các bài toán này.

Nếu bạn kém may mắn và gặp phải một vấn đề về quy hoạch động, bạn có thể giải quyết nó gần giống như cách giải quyết một bài toán đệ quy. Điểm khác nhau là những kết quả trung gian sẽ được lưu lại giúp cho việc tính toán sau này dễ dàng hơn.

***Lấy ví dụ về bài toán dãy số Fibonacci.***
Đây là bài toán rất cơ bản của các lập trình viên: 

> Tìm ra số Fibonacci thứ n

Đây là một giải pháp đơn giản sử dụng đệ quy:

```java
int findFibonacci(int i) { 
	if (i == 0) return 0;
	if (i == 1) return 1; 
	return findFibonacci(i - 1) + findFibonacci(i - 2); 
}
```

Nếu chúng ta xét tới độ phức tạp của giải pháp này, để tính ra được số Fibonacci thứ n, ta cần phải tính ra n-1 số trước, và mỗi số trước đó sẽ gọi đệ quy 2 lần. Điều này có nghĩa là độ phức tạp thuật toán là **O(2<sup>n</sup>)**. Đây là biểu đồ thể hiện thời gian chạy của thuật toán này theo n trên một máy tính bình thường

![Biểu đồ thời gian chạy Fibonacci]({{ "/images/ficonacci_runtime.PNG" | absolute_url }})

Nếu chúng ta thay đổi thuật toán này một chút, chúng ta có thể giảm độ phức tạp của thuật toán xuống còn **O(n)**. Chúng ta chỉ cần lưu lại các giá trị đã được tính của dãy Fibonacci.

```java
int[] fib = new int[max]; 
int findFibonacci(int i) { 
	if (i == 0) return 0; 
	if (i == 1) return 1;
	if (fib[i] != 0) return fib[i]; // Return cached result. 
	fib[i] = findFibonacci(i - 1) + findFibonacci(i - 2); // Cache result 
	return fib[i];
}
```
    
Trong khi pháp đầu tiên cần khoảng 1 phút để tìm ra số Fibonacci thứ 50 thì giải pháp sau có thể tìm ra số Fibonacci thứ  10,000 chỉ trong vòng chưa đển một mili giây (Tất nhiên, nếu sử dụng code y như trên thì kết quả sẽ bị tràn do sử dụng kiểu int).
Như bạn thấy, quy hoạch động không có gì đáng sợ. Nó chỉ tốt hơn đệ quy do lưu trữ lại các kết quả trước đó. Cách tốt nhất để thực hiện là dùng đệ quy để giải quyết như một bài toán đệ quy thông thường và sau đó nghĩ tới việc lưu trữ lại những kết quả đã được tính toán.

### So sánh giải pháp đệ quy và giải pháp tuần tự
Các giải pháp đệ quy thường rất tốn bộ nhớ. Mỗi lần gọi đệ quy, chương trình sẽ thêm một lớp vào bộ nhớ, nghĩa là nếu chúng ta có O(n) lần đệ quy thì chương trình của chúng ta sử dụng O(n) bộ nhớ.
Mọi giải pháp đệ quy đều có thể khử đệ quy thành một giải pháp tuần tự, nhưng việc chuyển đổi thường khá phức tạp. Trước khi bắt đầu giải pháp đệ quy, ta cần phải xét tới việc, sử dụng một giải pháp tuần tự cho bài toán có dễ không và thảo luận với người phỏng vấn.

### Một số bài toán áp dụng đệ quy

 1. Một cậu bé chạy lên một cầu thang có n bậc thang, và cậu bé này có thể bước 1, 2, hoặc 3 bậc thang một lần. Hãy tìm ra giải pháp để đếm được có bao nhiêu cách để cậu bé này chạy đến hết cầu thang.
 2. Hãy tưởng tượng một con robot đang ở góc trái trên trong một bản đồ các ô vuông tại vị trí (0,0). Robot này chỉ có thể đi qua phải và đi xuống. Có bao nhiêu cách để robot có thể đi tới điểm (X,Y).
	 *Nâng cao: Có một số ôtrong bản đồ robot không thể đi qua được, hãy thiết kế giải pháp để robot có thể đi từ điểm trái trên cùng đến điểm phải dưới cùng*
 3. Trong một mảng A[0...n-1], có một phần tử thứ i mà tại đó, A[i] = [i]. Biết rằng mảng đã được sắp xếp và các phần tử đều khác nhau. Hãy tìm ra i.
	*Nâng cao, thực hiện bài toán trên với mảng A có thể có các phần tử giống nhau*
 4. Tìm tất cả tập hơn con của một tập hợp
 5. Tìm tất cả các cách cách sắp xếp khác nhau của một chuỗi (ví dụ, chuỗi "ABC" có các cách sắp xếp: "ABC", "ACB", "BAC", "BCA", "CBA", "CAB")
 6. Tìm tất cả các cách kết hợp hợp lệ của n cặp dấu ngoặc đơn.
	 Ví dụ, với n = 3: ta có ( ( ( ) ) ), ( ( ) ( ) ), ( ) ( ( ) ), ( ( ) ) ( ), ( ) ( ) ( )
 7. Thiết kế giải thuật để thực hiện việc fill màu trên các phần mềm chỉnh sửa ảnh (chọn một màu và một điểm, toàn bộ vùng xung quanh điểm được chọn sẽ được tô màu được chọn)
 8. Tìm ra tất cả các cách để có n cent từ 25, 10, 5, 1 cent.
 9. Tìm giải pháp cho bài toán 8 con hậu (8 con hậu nằm trên bàn cờ sao cho các con hậu không thể ăn nhau từng đôi một.
 10. Có một n hộp, mỗi hộp có chiều cao, chiều dài và chiều rộng khác nhau. Một hộp chỉ có thể chồng lên hộp khác nếu chiều cao, chiều dài và chiều rộng của nó nhỏ hơn hộp trên cùng. Không được phép xoay các hộp, tìm ra cách để chồng các hộp sau cho tổng chiều cao của các hộp được chồng là cao nhất
 11. Cho một biểu thức gồm "**1**", "**0**", "**&**", "**|**", "**^**", tìm các cách biến đổi biểu thức đã cho bằng cách thêm vào các dấu ngoặc đơn để có thể được kết quả mong muốn
	 Ví dụ:
	 Biểu thức được cho: 1^0|0|1
	 Kết quả mong muốn: false (0)
	 Các cách biến đổi: 1^((0|0)|1) và 1^(0|(0|1))
