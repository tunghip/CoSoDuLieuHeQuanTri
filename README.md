# Quản lý sân bóng 

-Tác giả: Nguyễn Quý Tùng 
-MSSV:k215480106053
-Lớp: K57KMT
-Ngày làm: 2024-06-13
# Chức Năng Cơ Bản 
- 1.Quản lý 
- 1.1 Quản Lý Sân Bóng 
- Để quản lý sân bóng, bạn cần có các chức năng sau:

- Thêm sân bóng mới: Cho phép thêm thông tin của một sân bóng mới vào cơ sở dữ liệu

 - Sửa thông tin sân bóng: Cho phép chỉnh sửa thông tin của một sân bóng đã tồn tại trong cơ sở dữ liệu

- Xóa sân bóng: Cho phép xóa thông tin của một sân bóng khỏi cơ sở dữ liệu

- Xem danh sách sân bóng: Hiển thị danh sách tất cả các sân bóng có trong cơ sở dữ liệu
- 1.2 Quản Lý Đánh Giá 
- Thêm đánh giá mới: Cho phép thêm thông tin của một đánh giá mới vào cơ sở dữ liệu

- ReviewID: Khóa chính, số nguyên, tự động tăng (nếu sử dụng tự động tăng)
- PitchID: ID của sân bóng mà đánh giá được liên kết
- CustomerName: Tên của khách hàng đánh giá
- Rating: Điểm đánh giá từ khách hàng
- Comment: Bình luận của khách hàng (tùy chọn)
- Sửa thông tin đánh giá: Cho phép chỉnh sửa thông tin của một đánh giá đã tồn tại trong cơ sở dữ liệu
 
- Xóa đánh giá: Cho phép xóa thông tin của một đánh giá khỏi cơ sở dữ liệu

- Xem danh sách đánh giá: Hiển thị danh sách tất cả các đánh giá có trong cơ sở dữ liệu, bao gồm thông tin về sân bóng, khách hàng, điểm đánh giá và bình luận (nếu có)
- 1.3 Quản Lý Khách Hàng
- Thêm khách hàng: Cho phép thêm mới thông tin của một khách hàng vào cơ sở dữ liệu

- CustomerID: Khóa chính, số nguyên, tự động tăng (nếu sử dụng tự động tăng)
- CustomerName: Tên của khách hàng
- Email: Địa chỉ email của khách hàng
- Phone: Số điện thoại của khách hàng
- Sửa thông tin khách hàng: Cho phép chỉnh sửa thông tin của một khách hàng đã tồn tại trong cơ sở dữ liệu
 
- Xóa khách hàng: Cho phép xóa thông tin của một khách hàng khỏi cơ sở dữ liệu

- Xem danh sách khách hàng: Hiển thị danh sách tất cả các khách hàng có trong cơ sở dữ liệu, bao gồm thông tin về tên khách hàng, email và số điện thoại
- 2. Chức Năng Truy Vấn 
- Xem danh sách các sân bóng trong cơ sở dữ liệu:
- SELECT * FROM Pitch;
- Thêm một sân bóng mới vào cơ sở dữ liệu:
- INSERT INTO Pitch (PitchID, PitchName, Location, Capacity)
- VALUES (3, 'Sân C', 'Địa chỉ C', 4000);
- Chỉnh sửa thông tin của một sân bóng đã tồn tại:
- UPDATE Pitch
- SET Capacity = 4500
- WHERE PitchID = 1;
- Xóa thông tin của một sân bóng khỏi cơ sở dữ liệu:
- DELETE FROM Pitch
- WHERE PitchID = 3;
- Xem danh sách các trận đấu đã được lên lịch trên các sân bóng:
- SELECT Match.MatchID, Match.MatchDate, HomeTeam.TeamName AS HomeTeam, AwayTeam.TeamName AS AwayTeam, Pitch.PitchName
- FROM Match
- INNER JOIN Team AS HomeTeam ON Match.HomeTeamID = HomeTeam.TeamID
- INNER JOIN Team AS AwayTeam ON Match.AwayTeamID = AwayTeam.TeamID
- INNER JOIN Pitch ON Match.PitchID = Pitch.PitchID;
- Xem số lượng trận đấu đã diễn ra trên mỗi sân bóng:
- SELECT Pitch.PitchID, Pitch.PitchName, COUNT(*) AS NumMatches
- FROM Match
- JOIN Pitch ON Match.PitchID = Pitch.PitchID
- GROUP BY Pitch.PitchID, Pitch.PitchName;
- Xem thông tin về các đội bóng chơi trên sân bóng cụ thể:
- SELECT Team.TeamID, Team.TeamName, Team.Coach, Team.FoundedYear
- FROM Team
- WHERE Team.TeamID IN (SELECT DISTINCT HomeTeamID FROM Match UNION SELECT DISTINCT AwayTeamID FROM Match);
- Xem danh sách cầu thủ của một đội bóng cụ thể:
- SELECT Player.PlayerID, Player.PlayerName, Player.Position
- FROM Player
- WHERE Player.TeamID = 1; -- Thay 1 bằng TeamID của đội bóng muốn xem danh sách cầu thủ
- Xem các trận đấu của một đội bóng trong khoảng thời gian nhất định:
- SELECT Match.MatchID, Match.MatchDate, HomeTeam.TeamName AS HomeTeam, AwayTeam.TeamName AS AwayTeam, Pitch.PitchName
- FROM Match
- INNER JOIN Team AS HomeTeam ON Match.HomeTeamID = HomeTeam.TeamID
- INNER JOIN Team AS AwayTeam ON Match.AwayTeamID = AwayTeam.TeamID
- INNER JOIN Pitch ON Match.PitchID = Pitch.PitchID
- WHERE Match.MatchDate BETWEEN '2024-06-20' AND '2024-06-30';
- Xem các trận đấu mà một đội bóng cụ thể tham gia (làm đội chủ nhà hoặc đội khách):
- SELECT Match.MatchID, Match.MatchDate, HomeTeam.TeamName AS HomeTeam, AwayTeam.TeamName AS AwayTeam, Pitch.PitchName
- FROM Match
- INNER JOIN Team AS HomeTeam ON Match.HomeTeamID = HomeTeam.TeamID
- INNER JOIN Team AS AwayTeam ON Match.AwayTeamID = AwayTeam.TeamID
- INNER JOIN Pitch ON Match.PitchID = Pitch.PitchID
- WHERE HomeTeam.TeamID = 1 OR AwayTeam.TeamID = 1; -- Thay 1 bằng TeamID của đội bóng muốn xem
- 3.Chức Năng Nâng Cao
- 3.1 Trigger
- Cập nhật tổng số sao và số lượng đánh giá
Tự động cập nhật tổng số sao và số lượng đánh giá của một sân bóng khi có đánh giá mới được thêm vào hoặc khi một đánh giá bị xóa hoặc chỉnh sửa.
- CREATE OR ALTER TRIGGER UpdatePitchRating
ON Review
AFTER INSERT, DELETE, UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    DECLARE @PitchID INT;

    -- Lấy PitchID từ bảng Review
    IF EXISTS (SELECT 1 FROM inserted)
        SELECT @PitchID = PitchID FROM inserted;
    ELSE
        SELECT @PitchID = PitchID FROM deleted;

    -- Cập nhật tổng số sao và số lượng đánh giá
    UPDATE Pitch
    SET TotalStars = (
            SELECT SUM(Rating)
            FROM Review
            WHERE PitchID = @PitchID
        ),
        NumReviews = (
            SELECT COUNT(*)
            FROM Review
            WHERE PitchID = @PitchID
        )
    WHERE PitchID = @PitchID;
END;
- 3.2 Cursor
- Duyệt qua các sân bóng
Tạo thủ tục lưu trữ để duyệt qua các sân bóng và thực hiện các tính toán tổng hợp như số lượng trận đấu diễn ra trên mỗi sân bóng
- CREATE OR ALTER PROCEDURE CalculateMatchesPerPitch
AS
BEGIN
    DECLARE @PitchID INT;
    DECLARE @PitchName VARCHAR(50);
    DECLARE @MatchCount INT;

    DECLARE pitch_cursor CURSOR FOR
    SELECT PitchID, PitchName
    FROM Pitch;

    OPEN pitch_cursor;
    FETCH NEXT FROM pitch_cursor INTO @PitchID, @PitchName;

    WHILE @@FETCH_STATUS = 0
    BEGIN
        -- Tính số lượng trận đấu trên mỗi sân bóng
        SELECT @MatchCount = COUNT(*)
        FROM Match
        WHERE PitchID = @PitchID;

        -- In kết quả hoặc thực hiện các tính toán khác
        PRINT 'Sân ' + @PitchName + ' có ' + CAST(@MatchCount AS VARCHAR) + ' trận đấu.';

        FETCH NEXT FROM pitch_cursor INTO @PitchID, @PitchName;
    END;

    CLOSE pitch_cursor;
    DEALLOCATE pitch_cursor;
END;
- 3.3. Báo Cáo và Thống Kê
Báo cáo sân bóng phổ biến
Tạo báo cáo hiển thị các sân bóng phổ biến dựa trên số lượng trận đấu diễn ra trên mỗi sân bóng
- SELECT Pitch.PitchID, Pitch.PitchName, COUNT(Match.MatchID) AS NumMatches
FROM Pitch
LEFT JOIN Match ON Pitch.PitchID = Match.PitchID
GROUP BY Pitch.PitchID, Pitch.PitchName
ORDER BY NumMatches DESC;
## Thiết kế chương trình trong SQL
- 1.Tạo các bảng
- Bảng Pitch 

  ![image](https://github.com/tunghip/CoSoDuLieuHeQuanTri/assets/173240067/fa11f359-4f2d-4742-a36f-589cf2faf8d4)
- PitchID: Là khóa chính (Primary Key) của bảng, sử dụng để duy nhất xác định mỗi sân bóng
- PitchName: Tên sân bóng, không được phép để trống (NOT NULL)
- Location: Địa điểm của sân bóng
- Capacity: Sức chứa của sân bóng

- Bảng Match

  ![image](https://github.com/tunghip/CoSoDuLieuHeQuanTri/assets/173240067/aed63492-0636-4c97-8a65-4a7f70b3eeaf)

- MatchID: Là khóa chính của bảng, đại diện cho mỗi trận đấu
- MatchDate: Ngày diễn ra trận đấu, không được để trống
- HomeTeamID, AwayTeamID: Được sử dụng để tham chiếu đến đội chủ nhà và đội khách trong trận đấu, tham chiếu đến bảng Team
- PitchID: ID của sân bóng mà trận đấu diễn ra, tham chiếu đến bảng Pitch

- Bảng Team


  ![image](https://github.com/tunghip/CoSoDuLieuHeQuanTri/assets/173240067/a28c7c93-e2b4-469d-8fe7-3a57bf97273a)

- TeamID: Là khóa chính của bảng, đại diện cho mỗi đội bóng
- TeamName: Tên đội bóng, không được để trống
- Coach: Tên huấn luyện viên của đội bóng
- FoundedYear: Năm thành lập của đội bóng
  
- Bảng Player


  ![image](https://github.com/tunghip/CoSoDuLieuHeQuanTri/assets/173240067/2ac7b3a9-3081-4476-9014-40ef8cd3d6b2)

- PlayerID: Là khóa chính của bảng, đại diện cho mỗi cầu thủ
- PlayerName: Tên của cầu thủ, không được để trống
- TeamID: ID của đội bóng mà cầu thủ đó thuộc về, tham chiếu đến bảng Team
- Position: Vị trí chơi bóng của cầu thủ
- 2.Thêm dữ liệu các bảng
-- Thêm một sân bóng mới
  - INSERT INTO Pitch (PitchID, PitchName, Location, Capacity)
VALUES (1, 'Sân A', 'Địa chỉ A', 5000);
-- Thêm sân bóng khác
 -INSERT INTO Pitch (PitchID, PitchName, Location, Capacity)
VALUES (2, 'Sân B', 'Địa chỉ B', 3000);
-- Thêm trận đấu khác
 -INSERT INTO Match (MatchID, MatchDate, HomeTeamID, AwayTeamID, PitchID)
VALUES (2, '2024-06-22', 2, 1, 2);
-- Thêm đội bóng mới
- INSERT INTO Team (TeamID, TeamName, Coach, FoundedYear)
VALUES (1, 'Đội A', 'Huấn luyện viên A', 1990);
-- Thêm cầu thủ mới
  - INSERT INTO Player (PlayerID, PlayerName, TeamID, Position)
VALUES (1, 'Cầu thủ A', 1, 'Tiền đạo');
-- Thêm cầu thủ khác
 - INSERT INTO Player (PlayerID, PlayerName, TeamID, Position)
VALUES (2, 'Cầu thủ B', 2, 'Trung vệ');
# Thiết lập chức năng 
- 1.Chức năng cơ bản
- 1.1.Chức năng tìm thêm, xoá, sửa thông tin
-  INSERT INTO Pitch (PitchID, PitchName, Location, Capacity)
VALUES (...);
- Thêm sân bóng: Cho phép thêm mới thông tin về các sân bóng vào cơ sở dữ liệu
- UPDATE Pitch
SET ...
WHERE PitchID = ...;
- Sửa thông tin sân bóng: Cho phép chỉnh sửa thông tin của các sân bóng đã tồn tại trong cơ sở dữ liệu
- DELETE FROM Pitch
WHERE PitchID = ...;
- Xóa sân bóng: Cho phép xóa thông tin về các sân bóng khỏi cơ sở dữ liệu, ví dụ khi sân bóng không còn hoạt động nữa
- SELECT * FROM Pitch;
Xem danh sách sân bóng: Hiển thị danh sách các sân bóng hiện có trong cơ sở dữ liệu
- 2.Chức năng nâng cao
- Tự động cập nhật số trận và chất lượng đánh giá của một sân bóng
- CREATE TRIGGER PreventPitchDelete
ON Pitch
INSTEAD OF DELETE
AS
BEGIN
    SET NOCOUNT ON;

    DECLARE @numMatches INT;
    SELECT @numMatches = COUNT(*) FROM Match WHERE PitchID = (SELECT PitchID FROM deleted);

    IF @numMatches > 0
    BEGIN
        RAISERROR('Cannot delete pitch because matches are scheduled on this pitch.', 16, 1);  -- Sửa từ RAISEERROR thành RAISERROR
    END
    ELSE
    BEGIN
        DELETE FROM Pitch WHERE PitchID IN (SELECT PitchID FROM deleted);  -- Sửa thành DELETE ... WHERE PitchID IN (SELECT ...)
    END
END;

- Tìm kiếm thông tin
-- Tạo một VIEW mới có tên 'View_San Bong' hiển thị lượng khách của sân
- -- Tạo VIEW View_SanBong
CREATE VIEW View_SanBong AS
SELECT Pitch.PitchID, Pitch.PitchName, Pitch.Location, COUNT(Match.MatchID) AS NumMatches
FROM Pitch
LEFT JOIN Match ON Pitch.PitchID = Match.PitchID
GROUP BY Pitch.PitchID, Pitch.PitchName, Pitch.Location;

  
