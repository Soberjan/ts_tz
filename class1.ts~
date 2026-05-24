/**
 * Простая точка в 2D-пространстве.
 */
export class Point {
  /** X-координата */
  public readonly x: number;
  /** Y-координата */
  public readonly y: number;

  /**
   * Создаёт точку.
   * @param x - X-координата
   * @param y - Y-координата
   */
  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}

/**
 * Интерфейс общей фигуры.
 */
export interface IShape {
  /**
   * Вычислить площадь фигуры.
   * @returns площадь (число >= 0)
   */
  area(): number;
}

/**
 * Абстрактный базовый класс для полигона.
 * Хранит вершины и предоставляет сортировку по обходу.
 */
export abstract class Polygon implements IShape {
  /** Вершины полигона */
  protected vertices: Point[];

  /**
   * @param vertices - массив вершин (любого порядка). Должно быть >= 3 вершин.
   */
  constructor(vertices: Point[]) {
    if (vertices.length < 3) throw new Error("Polygon requires at least 3 vertices");
    this.vertices = vertices.slice();
  }

  /**
   * Сортирует this.vertices по часовой стрелке относительно центроида.
   * Защищённый метод — может быть переопределён в подклассах при необходимости.
   */
  protected sortClockwise(): void {
    this.sortClockwise();
    const pts = this.vertices;
    const cx = pts.reduce((s, p) => s + p.x, 0) / pts.length;
    const cy = pts.reduce((s, p) => s + p.y, 0) / pts.length;
    this.vertices = pts.slice().sort((a, b) => {
      const angA = Math.atan2(a.y - cy, a.x - cx);
      const angB = Math.atan2(b.y - cy, b.x - cx);
      return angB - angA; // descending => clockwise
    });
  }

  /**
   * Вычисляет площадь полигона методом Гаусса (shoelace).
   * Требует, чтобы вершины были в порядке обхода.
   * @returns площадь полигона
   */
  public area(): number {
    const pts = this.vertices;
    let sum = 0;
    for (let i = 0; i < pts.length; i++) {
      const p1 = pts[i];
      const p2 = pts[(i + 1) % pts.length];
      sum += p1.x * p2.y - p2.x * p1.y;
    }
    return Math.abs(sum) / 2;
  }
}

/**
 * Треугольник 
 */
export class Triangle extends Polygon {
  /**
   * Создаёт треугольник.
   * @param vertices - кортеж из трёх точек
   */
  constructor(vertices: [Point, Point, Point]) {
    super(vertices);
  }
}

/**
 * Прямоугольник (ровно 4 вершины).
 */
export class Rectangle extends Polygon {
  constructor(vertices: [Point, Point, Point, Point], tol = 1e-6) {
    super(vertices);
  }
}

/**
 * Круг.
 */
export class Circle implements IShape {
  /** Радиус круга (>= 0) */
  public readonly radius: number;

  /**
   * @param radius - радиус круга
   */
  constructor(radius: number) {
    if (radius < 0) throw new Error("Radius must be >= 0");
    this.radius = radius;
  }

  /** Площадь круга. */
  public area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

/* Пример использования */
const t = new Triangle([new Point(0, 0), new Point(0, 1), new Point(1, 0)]);
console.log(t.area()); // 0.5

const r = new Rectangle([new Point(0, 0), new Point(0, 1), new Point(1, 1), new Point(1, 0)]);
console.log(r.area()); // 1

const c = new Circle(10);
console.log(c.area()); // ~314.159...
