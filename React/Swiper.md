# Swiper

ライブラリを導入することでスライダーを実装可能。
Vue, React, Angular全てに対応。

- [https://swiperjs.com/](https://swiperjs.com/)

## install swiper

    ``` bash
    yarn add swiper
    ```

## emplement swiper

    ``` tsx
    // Import Swiper React components
    import { Swiper, SwiperSlide } from 'swiper/react';

    // Import Swiper styles
    import 'swiper/css';

    export default () => {
        return (
            <Swiper>
            <SwiperSlide>Slide 1</SwiperSlide>
            <SwiperSlide>Slide 2</SwiperSlide>
            <SwiperSlide>Slide 3</SwiperSlide>
            </Swiper>
        );
    };
    ```
