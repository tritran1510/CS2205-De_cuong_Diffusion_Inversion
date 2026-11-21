# Cải tiến cơ chế khởi tạo của InvSR dựa trên thông tin nén JPEG cho bài toán siêu phân giải ảnh

*Improving InvSR Initialization Using JPEG Compression Information for Image Super-Resolution*

Đề cương nghiên cứu môn **CS2205 - Phương pháp luận nghiên cứu khoa học**, lớp **CS2205.AUG2026**.

- Học viên: **TRẦN HỮU TRÍ - MSHV 26848231**.
- Giảng viên: PGS.TS. Lê Đình Duy.
- Trường Đại học Công nghệ Thông tin, ĐHQG-HCM.
- Repository: [tritran1510/CS2205-De_cuong_Diffusion_Inversion](https://github.com/tritran1510/CS2205-De_cuong_Diffusion_Inversion).

## Tài liệu chỉnh sửa

| Tài liệu | File |
|---|---|
| Đề cương chi tiết | [Word DOCX](CS2205_DeCuong_InvSR/CS2205.DeCuong.InvSR.docx) |
| Slide thuyết trình | [PowerPoint PPTX](CS2205_DeCuong_InvSR/CS2205.DeCuong.InvSR.TranHuuTri.pptx) |
| Poster theo bố cục Navy | [PowerPoint PPTX](CS2205_DeCuong_InvSR/CS2205.InvSR.Poster.TranHuuTri.pptx) |

Đề cương gồm 1 trang thông tin và 5 trang nội dung. Slide gồm 10 trang; poster gồm 1 trang. Bộ nộp trên GitHub gồm ba tài liệu trong bảng. Slide để nộp không chứa lời thoại trong Notes. Bản có script được giữ riêng trên máy để tập thuyết trình.

**Video trình bày:** sẽ được bổ sung sau khi học viên tự quay.

## Tóm tắt

Ảnh được thu nhỏ rồi nén JPEG có thể mất đường biên mảnh, họa tiết và lộ khối nén khi phóng lớn. InvSR dùng một mạng dự đoán nhiễu để tạo trạng thái bắt đầu cho quá trình phục hồi bằng mô hình khuếch tán (diffusion). InvSR gốc đã được huấn luyện với dữ liệu mô phỏng JPEG. Phần cải tiến dự kiến là một nhánh nhỏ nhận đặc trưng ảnh và bảng lượng tử của chính tệp JPEG, rồi học phần điều chỉnh cộng vào nhiễu khởi tạo.

Trong huấn luyện, ảnh phục hồi được thu nhỏ lại theo đúng phép tạo dữ liệu. Các hệ số DCT của ảnh thu nhỏ được đối chiếu với khoảng giá trị suy ra từ bảng lượng tử và hệ số DCT đã lượng tử trong tệp đầu vào; chỉ phần vượt khoảng mới bị phạt. Nhánh mới sẽ được kiểm chứng bằng so sánh với InvSR gốc, fine-tune thông thường và các cấu hình bỏ từng thành phần. Kết luận dựa trên chất lượng so với ảnh HR tham chiếu, mức phù hợp với thông tin nén và chi phí tính toán. Đây là đề cương; hiệu quả của phương pháp đề xuất chưa được khẳng định bằng kết quả thực nghiệm.

## Ba mục tiêu

1. Xây dựng quy trình đánh giá siêu phân giải JPEG ×4 và xác định sai lệch chất lượng, mức phù hợp với đầu vào cùng chi phí của InvSR gốc.
2. Đề xuất và huấn luyện nhánh hiệu chỉnh khởi tạo dựa trên thông tin nén, nhằm tăng độ trung thực với chi phí suy luận bổ sung được kiểm soát.
3. Kiểm chứng đóng góp bằng đối chứng và thí nghiệm bỏ thành phần, gồm đánh giá trên ảnh và mức nén chưa dùng khi học.

## Phương pháp và kết quả dự kiến

Dữ liệu chính là DIV2K, với ảnh HR thu nhỏ bicubic ×4 rồi nén JPEG 4:4:4 một lần. Ảnh nguồn được tách theo tập trước khi tạo vùng cắt. Các cấu hình học thêm dùng cùng ngân sách; checkpoint InvSR gốc được giữ làm mốc, không huấn luyện lại.

Đầu ra dự kiến gồm bộ ảnh ghép cặp và metadata, mô-đun hiệu chỉnh cùng trọng số sau huấn luyện, mã thực nghiệm, bảng PSNR/SSIM/LPIPS, mức phù hợp JPEG và chi phí, cùng ảnh cắt tại cùng tọa độ để phân tích chi tiết. Bảng chỉ điền số liệu sau khi chạy thực tế theo cùng giao thức. Kết luận sẽ nêu cả lợi ích, chi phí bổ sung và các trường hợp chưa cải thiện.

## Bài báo nền

Zongsheng Yue, Kang Liao, Chen Change Loy: **Arbitrary-steps Image Super-resolution via Diffusion Inversion.** CVPR 2025: 23153-23163.

[Bài báo](https://arxiv.org/abs/2412.09013) · [Mã nguồn InvSR của tác giả](https://github.com/zsyOAOA/InvSR)

Hình minh họa từ bài báo có ghi nguồn trong slide. Nhánh hiệu chỉnh theo thông tin JPEG là hướng nghiên cứu dự kiến của đề tài, phân biệt với InvSR gốc. Danh mục 8 công trình liên quan được ghi theo cấu trúc DBLP trong đề cương.
