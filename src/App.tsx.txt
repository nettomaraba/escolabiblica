import { useState } from "react";

const images = Array.from({ length: 12 }, (_, index) => {
  return `${import.meta.env.BASE_URL}img/${index + 1}.jpg`;
});

export default function App() {
  const [currentSlide, setCurrentSlide] = useState(0);

  function nextSlide() {
    setCurrentSlide((current) =>
      current < images.length - 1 ? current + 1 : current
    );
  }

  function previousSlide() {
    setCurrentSlide((current) => (current > 0 ? current - 1 : current));
  }

  return (
    <main className="slideshow">
      <div className="progress">
        {images.map((_, index) => (
          <div
            key={index}
            className={`progress-segment ${
              index === currentSlide ? "active" : ""
            }`}
          />
        ))}
      </div>

      <img
        className="slide-image"
        src={images[currentSlide]}
        alt={`Slide ${currentSlide + 1}`}
        draggable={false}
      />

      <button
        className="tap-zone left"
        onClick={previousSlide}
        aria-label="Imagem anterior"
      />

      <button
        className="tap-zone right"
        onClick={nextSlide}
        aria-label="Próxima imagem"
      />

      <div className="counter">
        {currentSlide + 1} / {images.length}
      </div>
    </main>
  );
}
