# Schema

    -- User Roles Table
    CREATE TABLE roles (
        role_id SERIAL PRIMARY KEY,
        role_name VARCHAR(50) NOT NULL,
        description TEXT,
        privileges JSONB
    );

    Note: Not sure how to deal with lanugages yet (should be alternate version for difference lang.)

    -- Users Table
    CREATE TABLE users (
        user_id SERIAL PRIMARY KEY,
        username VARCHAR(50) UNIQUE NOT NULL,
        password VARCHAR(255) NOT NULL,
        email VARCHAR(100) UNIQUE NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        language VARCHAR(20),
        theme VARCHAR(20),
        role_id INT NOT NULL,
        points INT DEFAULT 0,
        FOREIGN KEY (role_id) REFERENCES roles(role_id)
    );

    -- Tags Table
    CREATE TABLE tags (
        tag_id SERIAL PRIMARY KEY,
        tag_name VARCHAR(50) UNIQUE NOT NULL,
        description TEXT
    );

    -- Articles Table
    CREATE TABLE articles (
        article_id SERIAL PRIMARY KEY,
        user_id INT NOT NULL,
        title VARCHAR(255) NOT NULL,
        content TEXT NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        view_count INT DEFAULT 0,
        like_count INT DEFAULT 0,
        FOREIGN KEY (user_id) REFERENCES users(user_id)
    );

    -- Article_Tags Junction Table
    CREATE TABLE article_tags (
        article_id INT NOT NULL,
        tag_id INT NOT NULL,
        FOREIGN KEY (article_id) REFERENCES articles(article_id),
        FOREIGN KEY (tag_id) REFERENCES tags(tag_id)
    );

    -- Article Images Table
    CREATE TABLE article_images (
        image_id SERIAL PRIMARY KEY,
        article_id INT NOT NULL,
        image_url VARCHAR(255) NOT NULL,
        FOREIGN KEY (article_id) REFERENCES articles(article_id)
    );

    -- Article Glossary Table
    CREATE TABLE article_glossary (
        article_id INT NOT NULL,
        term_id INT NOT NULL,
        FOREIGN KEY (article_id) REFERENCES articles(article_id),
        FOREIGN KEY (term_id) REFERENCES glossary(term_id)
    );

    -- Glossary Table
    CREATE TABLE glossary (
        term_id SERIAL PRIMARY KEY,
        term VARCHAR(50) NOT NULL,
        definition TEXT NOT NULL,
        sample_code TEXT
    );

    # Note: not sure how to deal with this yet
    -- Annotations Table
    CREATE TABLE annotations (
        annotation_id SERIAL PRIMARY KEY,
        article_id INT NOT NULL,
        user_id INT NOT NULL,
        content TEXT NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (article_id) REFERENCES articles(article_id),
        FOREIGN KEY (user_id) REFERENCES users(user_id)
    );

    # Notes: There might need to be seperate table for reply and comment to a reply
    -- Comments Table for Forum
    CREATE TABLE comments (
        comment_id SERIAL PRIMARY KEY,
        article_id INT NOT NULL,
        user_id INT NOT NULL,
        content TEXT NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        parent_comment_id INT,
        image_urls JSONB,
        like_count INT DEFAULT 0,
        FOREIGN KEY (article_id) REFERENCES articles(article_id),
        FOREIGN KEY (user_id) REFERENCES users(user_id),
        FOREIGN KEY (parent_comment_id) REFERENCES comments(comment_id)
    );

    -- Feedback Table
    CREATE TABLE feedback (
        feedback_id SERIAL PRIMARY KEY,
        user_id INT NOT NULL,
        content TEXT NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (user_id) REFERENCES users(user_id)
    );

    -- Infographics Table (You would store info related to any infographics used in articles here)
    CREATE TABLE infographics (
        infographic_id SERIAL PRIMARY KEY,
        article_id INT NOT NULL,
        path VARCHAR(255) NOT NULL,
        description TEXT,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (article_id) REFERENCES articles(article_id)
    );

    -- Badges Table
    CREATE TABLE badges (
        badge_id SERIAL PRIMARY KEY,
        name VARCHAR(50) NOT NULL,
        description TEXT
    );

    -- User_Badges Junction Table
    CREATE TABLE user_badges (
        user_id INT NOT NULL,
        badge_id INT NOT NULL,
        awarded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (user_id) REFERENCES users(user_id),
        FOREIGN KEY (badge_id) REFERENCES badges(badge_id)
    );

    -- Bookmarks Table
    CREATE TABLE bookmarks (
        bookmark_id SERIAL PRIMARY KEY,
        user_id INT NOT NULL,
        article_id INT NOT NULL,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY (user_id) REFERENCES users(user_id),
        FOREIGN KEY (article_id) REFERENCES articles(article_id)
    );

# Custom Indexes
