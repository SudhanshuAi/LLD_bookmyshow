## Users Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| email      | VARCHAR(255) | UNIQUE |
| phone      | VARCHAR(20) | UNIQUE |
| name       | VARCHAR(255) |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Events Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| name       | VARCHAR(255) |  |
| type       | ENUM('MOVIE', 'SHOW', 'COMEDY') |  |
| description | TEXT |  |
| duration_mins | INTEGER |  |
| language   | VARCHAR(50) |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Venues Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| name       | VARCHAR(255) |  |
| address    | TEXT |  |
| city_id    | UUID | FOREIGN KEY → cities(id) |
| total_seats | INTEGER |  |
| seat_layout | JSONB |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Shows Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| event_id   | UUID | FOREIGN KEY → events(id) |
| venue_id   | UUID | FOREIGN KEY → venues(id) |
| show_time  | TIMESTAMP |  |
| price_config | JSONB |  |
| status     | ENUM('ACTIVE', 'CANCELLED', 'COMPLETED') |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Seats Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| show_id    | UUID | FOREIGN KEY → shows(id) |
| seat_number | VARCHAR(10) |  |
| category   | VARCHAR(50) |  |
| price      | DECIMAL(10,2) |  |
| status     | ENUM('AVAILABLE', 'LOCKED', 'BOOKED') |  |
| lock_expires_at | TIMESTAMP |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Bookings Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| user_id    | UUID | FOREIGN KEY → users(id) |
| show_id    | UUID | FOREIGN KEY → shows(id) |
| total_amount | DECIMAL(10,2) |  |
| status     | ENUM('PENDING', 'CONFIRMED', 'CANCELLED') |  |
| payment_id | UUID |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |

## Booking Seats Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| booking_id | UUID | FOREIGN KEY → bookings(id) |
| seat_id    | UUID | FOREIGN KEY → seats(id) |
| price      | DECIMAL(10,2) |  |
| created_at | TIMESTAMP |  |

## Payments Table
| Column Name | Data Type | Constraints |
|------------|-----------|-------------|
| id         | UUID      | PRIMARY KEY |
| booking_id | UUID | FOREIGN KEY → bookings(id) |
| amount     | DECIMAL(10,2) |  |
| payment_method | VARCHAR(50) |  |
| status     | ENUM('PENDING', 'SUCCESS', 'FAILED') |  |
| transaction_id | VARCHAR(255) |  |
| created_at | TIMESTAMP |  |
| updated_at | TIMESTAMP |  |
