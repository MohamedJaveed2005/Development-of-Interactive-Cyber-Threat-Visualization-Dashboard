DROP DATABASE IF EXISTS cyber_dashboard;
CREATE DATABASE cyber_dashboard;
USE cyber_dashboard;
CREATE TABLE ip_details (
    ip_id INT PRIMARY KEY,
    ip_address VARCHAR(45),
    country VARCHAR(50),
    is_malicious BOOLEAN
);

CREATE TABLE attacks (
    attack_id INT PRIMARY KEY,
    ip_id INT,
    attack_type VARCHAR(50),
    attack_time TIMESTAMP,
    severity INT,
    FOREIGN KEY (ip_id) REFERENCES ip_details(ip_id)
);

INSERT INTO ip_details VALUES
(1, '192.168.1.10', 'India', TRUE),
(2, '10.0.0.5', 'USA', FALSE),
(3, '172.16.0.8', 'Germany', TRUE),
(4, '8.8.8.8', 'USA', FALSE);

INSERT INTO attacks VALUES
(101, 1, 'Brute Force', '2026-02-12 10:00:00', 5),
(102, 2, 'SQL Injection', '2026-02-12 10:05:00', 4),
(103, 1, 'Ransomware', '2026-02-12 10:10:00', 5),
(104, 3, 'Phishing', '2026-02-12 10:15:00', 3),
(105, 1, 'Brute Force', '2026-02-12 10:20:00', 5);

SELECT * FROM ip_details;
SELECT * FROM attacks;

SELECT * FROM attacks
WHERE severity >= 4;

SELECT a.attack_id, i.ip_address, a.attack_type, a.severity
FROM attacks a
JOIN ip_details i
ON a.ip_id = i.ip_id;

SELECT DISTINCT attack_type
FROM attacks;

SELECT COUNT(*) AS total_attacks
FROM attacks;

SELECT attack_type, COUNT(*) AS total
FROM attacks
GROUP BY attack_type;

SELECT * FROM attacks
ORDER BY severity DESC;

SELECT attack_type, COUNT(*)
FROM attacks
GROUP BY attack_type
HAVING COUNT(*) > 1;
