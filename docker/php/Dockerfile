FROM php:8.3-fpm

# Dependências do sistema
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    curl \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libicu-dev \
    libxml2-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) \
        pdo_mysql \
        bcmath \
        gd \
        intl \
        opcache \
        zip \
        xml \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Extensão Redis
RUN pecl install redis \
    && docker-php-ext-enable redis

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Diretório de trabalho
WORKDIR /var/www

# Usuário padrão do PHP-FPM
EXPOSE 9000

CMD ["php-fpm"]
