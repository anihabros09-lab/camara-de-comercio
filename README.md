<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Cámara de Comercio — Directorio Empresarial</title>
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:wght@600;700&display=swap" rel="stylesheet" />
  <!-- Font Awesome -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />

  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            navy: {
              800: '#16284c',
              900: '#0f1c36',
              950: '#091224',
            },
            gold: {
              400: '#fbbf24',
              500: '#d97706',
              600: '#b45309',
            }
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Playfair Display', 'serif'],
          }
        }
      }
    }
  </script>

  <style>
    body {
      font-family: 'Inter', sans-serif;
      background-color: #f8fafc;
    }
    .hero-pattern {
      background-color: #0f1c36;
      background-image: radial-gradient(rgba(251, 191, 36, 0.12) 1px, transparent 1px);
      background-size: 24px 24px;
    }
    /* Custom scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
      height: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #f1f5f9;
    }
    ::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    .card-hover {
      transition: transform 0.25s ease, box-shadow 0.25s ease;
    }
    .card-hover:hover {
      transform: translateY(-4px);
      box-shadow: 0 12px 24px -8px rgba(15, 28, 54, 0.15);
    }
  </style>
</head>
<body class="text-slate-800 antialiased flex flex-col min-h-screen">

  <!-- Barra de navegación superior -->
  <header class="bg-navy-900 text-white sticky top-0 z-40 shadow-md border-b border-navy-800">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
      <div class="flex items-center space-x-3">
        <div class="w-11 h-11 rounded-lg bg-gradient-to-br from-amber-400 to-amber-600 flex items-center justify-center text-navy-950 shadow-lg">
          <i class="fa-solid fa-landmark text-xl"></i>
        </div>
        <div>
          <span class="font-serif text-xl sm:text-2xl font-bold tracking-tight block leading-none">
            Cámara de Comercio
          </span>
          <span class="text-xs text-amber-400 uppercase tracking-widest font-medium">
            Directorio Oficial de Afiliados
          </span>
        </div>
      </div>

      <div class="flex items-center space-x-3">
        <button
          onclick="openRegisterModal()"
          class="bg-amber-500 hover:bg-amber-400 text-navy-950 font-semibold px-4 py-2.5 rounded-lg text-sm transition flex items-center gap-2 shadow-sm cursor-pointer"
        >
          <i class="fa-solid fa-plus"></i>
          <span class="hidden sm:inline">Registrar Negocio</span>
          <span class="sm:hidden">Registrar</span>
        </button>
      </div>
    </div>
  </header>

  <!-- Sección Hero y Buscador -->
  <section class="hero-pattern text-white py-14 sm:py-20 px-4 border-b-4 border-amber-500">
    <div class="max-w-4xl mx-auto text-center">
      <span class="inline-block py-1 px-3 rounded-full bg-navy-800 border border-amber-500/30 text-amber-400 text-xs font-semibold uppercase tracking-wider mb-4">
        Impulsando el desarrollo económico local
      </span>
      <h1 class="font-serif text-3xl sm:text-5xl font-bold mb-4 leading-tight">
        Encuentra los mejores comercios y servicios afiliados
      </h1>
      <p class="text-slate-300 text-base sm:text-lg mb-8 max-w-2xl mx-auto">
        Explora empresas verificadas, conoce sus instalaciones, contacta directamente y descubre su ubicación exacta.
      </p>

      <!-- Barra de búsqueda -->
      <div class="bg-white p-2 rounded-xl shadow-2xl flex flex-col sm:flex-row gap-2 max-w-3xl mx-auto">
        <div class="relative flex-1 flex items-center">
          <i class="fa-solid fa-magnifying-glass text-slate-400 ml-3.5"></i>
          <input
            type="text"
            id="searchInput"
            placeholder="Buscar por nombre, servicio (ej. cafetería, diseño, reparación) o zona..."
            class="w-full pl-3 pr-4 py-3 text-slate-800 placeholder-slate-400 focus:outline-none text-sm sm:text-base rounded-lg"
            oninput="filterBusinesses()"
          />
          <button
            id="clearSearchBtn"
            onclick="clearSearch()"
            class="hidden text-slate-400 hover:text-slate-600 px-3 cursor-pointer"
            title="Limpiar búsqueda"
          >
            <i class="fa-solid fa-xmark"></i>
          </button>
        </div>
        <select
          id="categorySelect"
          onchange="filterBusinesses()"
          class="bg-slate-100 text-slate-700 font-medium text-sm px-4 py-3 rounded-lg border-0 focus:ring-2 focus:ring-amber-500 outline-none cursor-pointer"
        >
          <option value="Todos">Todas las categorías</option>
          <option value="Gastronomía">Gastronomía</option>
          <option value="Tecnología">Tecnología</option>
          <option value="Salud y Bienestar">Salud y Bienestar</option>
          <option value="Construcción y Hogar">Construcción y Hogar</option>
          <option value="Servicios Profesionales">Servicios Profesionales</option>
          <option value="Comercio Minorista">Comercio Minorista</option>
        </select>
      </div>
    </div>
  </section>

  <!-- Contenido Principal -->
  <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-10">
    <!-- Barra de estado y filtros rápidos -->
    <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 mb-8 pb-4 border-b border-slate-200">
      <div>
        <h2 class="text-xl font-bold text-navy-900">Negocios Afiliados</h2>
        <p class="text-sm text-slate-500" id="resultsCount">Mostrando negocios registrados</p>
      </div>

      <!-- Chips de categorías rápidas -->
      <div class="flex items-center gap-2 overflow-x-auto pb-1" id="categoryPills">
        <button onclick="setCategory('Todos')" data-cat="Todos" class="cat-pill active px-3.5 py-1.5 rounded-full text-xs font-semibold bg-navy-900 text-white transition cursor-pointer whitespace-nowrap">
          Todos
        </button>
        <button onclick="setCategory('Gastronomía')" data-cat="Gastronomía" class="cat-pill px-3.5 py-1.5 rounded-full text-xs font-semibold bg-white text-slate-600 border border-slate-200 hover:border-navy-800 transition cursor-pointer whitespace-nowrap">
          Gastronomía
        </button>
        <button onclick="setCategory('Tecnología')" data-cat="Tecnología" class="cat-pill px-3.5 py-1.5 rounded-full text-xs font-semibold bg-white text-slate-600 border border-slate-200 hover:border-navy-800 transition cursor-pointer whitespace-nowrap">
          Tecnología
        </button>
        <button onclick="setCategory('Salud y Bienestar')" data-cat="Salud y Bienestar" class="cat-pill px-3.5 py-1.5 rounded-full text-xs font-semibold bg-white text-slate-600 border border-slate-200 hover:border-navy-800 transition cursor-pointer whitespace-nowrap">
          Salud y Bienestar
        </button>
        <button onclick="setCategory('Construcción y Hogar')" data-cat="Construcción y Hogar" class="cat-pill px-3.5 py-1.5 rounded-full text-xs font-semibold bg-white text-slate-600 border border-slate-200 hover:border-navy-800 transition cursor-pointer whitespace-nowrap">
          Construcción y Hogar
        </button>
      </div>
    </div>

    <!-- Cuadrícula de Tarjetas de Negocios -->
    <div id="businessGrid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-7">
      <!-- Las tarjetas se renderizan dinámicamente con JavaScript -->
    </div>

    <!-- Estado vacío si no hay resultados -->
    <div id="emptyState" class="hidden text-center py-16 bg-white rounded-2xl border border-slate-200 shadow-sm">
      <div class="w-16 h-16 bg-slate-100 text-slate-400 rounded-full flex items-center justify-center mx-auto mb-4">
        <i class="fa-solid fa-store-slash text-2xl"></i>
      </div>
      <h3 class="text-lg font-bold text-navy-900 mb-1">No se encontraron negocios</h3>
      <p class="text-slate-500 text-sm max-w-md mx-auto mb-5">
        No hay comercios que coincidan con tu búsqueda o categoría seleccionada. Intenta con otros términos o registra un nuevo local.
      </p>
      <button onclick="resetFilters()" class="px-4 py-2 bg-navy-900 text-white text-sm font-medium rounded-lg hover:bg-navy-800 transition cursor-pointer">
        Restablecer filtros
      </button>
    </div>
  </main>

  <!-- Pie de página -->
  <footer class="bg-navy-950 text-slate-400 py-10 px-4 mt-12 border-t border-navy-800">
    <div class="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
      <div class="flex items-center space-x-2">
        <i class="fa-solid fa-landmark text-amber-500"></i>
        <span class="font-serif text-white font-semibold">Cámara de Comercio Local</span>
      </div>
      <p class="text-xs text-center sm:text-right">
        © 2026 Directorio Oficial de Empresas y Servicios. Todos los derechos reservados.
      </p>
    </div>
  </footer>

  <!-- ==========================================
       MODAL 1: DETALLE DEL NEGOCIO Y GALERÍA
  =========================================== -->
  <div id="detailModal" class="fixed inset-0 z-50 hidden bg-navy-950/75 backdrop-blur-sm flex items-center justify-center p-4 overflow-y-auto">
    <div class="bg-white rounded-2xl max-w-3xl w-full overflow-hidden shadow-2xl border border-slate-200 my-auto animate-fadeIn">
      <!-- Galería de Fotos del Local -->
      <div class="relative bg-slate-900">
        <button
          onclick="closeDetailModal()"
          class="absolute top-4 right-4 z-10 w-9 h-9 rounded-full bg-black/60 hover:bg-black/80 text-white flex items-center justify-center transition cursor-pointer"
          title="Cerrar"
        >
          <i class="fa-solid fa-xmark"></i>
        </button>

        <!-- Imagen principal -->
        <div class="h-64 sm:h-80 w-full overflow-hidden relative">
          <img id="modalMainImage" src="" alt="Foto del local" class="w-full h-full object-cover transition duration-300" />
          <div class="absolute bottom-3 left-4 bg-black/65 backdrop-blur-xs text-white text-xs px-3 py-1 rounded-full">
            <i class="fa-solid fa-camera mr-1.5 text-amber-400"></i>
            <span id="modalPhotoCounter">Foto 1 de 3</span>
          </div>
        </div>

        <!-- Miniaturas de fotos del local -->
        <div id="modalThumbnails" class="flex gap-2 p-3 bg-navy-950 overflow-x-auto">
          <!-- Miniaturas inyectadas dinámicamente -->
        </div>
      </div>

      <!-- Información del Negocio -->
      <div class="p-6 sm:p-8">
        <div class="flex flex-wrap items-center justify-between gap-2 mb-2">
          <span id="modalCategory" class="px-3 py-1 rounded-full text-xs font-semibold bg-amber-100 text-amber-800">
            Categoría
          </span>
          <span class="text-xs text-emerald-600 font-semibold flex items-center gap-1">
            <i class="fa-solid fa-circle-check"></i> Afiliado Verificado
          </span>
        </div>

        <h2 id="modalName" class="font-serif text-2xl sm:text-3xl font-bold text-navy-900 mb-3">
          Nombre del Negocio
        </h2>

        <p id="modalDescription" class="text-slate-600 text-sm sm:text-base mb-6 leading-relaxed">
          Descripción detallada del negocio...
        </p>

        <!-- Datos de Contacto y Ubicación -->
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6 bg-slate-50 p-4 rounded-xl border border-slate-200/80">
          <div class="flex items-start gap-3">
            <div class="w-9 h-9 rounded-lg bg-navy-900 text-amber-400 flex items-center justify-center shrink-0 mt-0.5">
              <i class="fa-solid fa-phone"></i>
            </div>
            <div>
              <span class="text-xs text-slate-500 block font-medium">Teléfono de Contacto</span>
              <a id="modalPhoneLink" href="#" class="text-navy-900 font-bold hover:text-amber-600 transition text-sm sm:text-base">
                +52 55 1234 5678
              </a>
            </div>
          </div>

          <div class="flex items-start gap-3">
            <div class="w-9 h-9 rounded-lg bg-navy-900 text-amber-400 flex items-center justify-center shrink-0 mt-0.5">
              <i class="fa-solid fa-location-dot"></i>
            </div>
            <div>
              <span class="text-xs text-slate-500 block font-medium">Lugar donde se localiza</span>
              <span id="modalLocation" class="text-navy-900 font-semibold text-sm block">
                Dirección del local
              </span>
              <a
                id="modalMapLink"
                href="#"
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center gap-1 text-xs font-semibold text-amber-600 hover:text-amber-700 mt-1"
              >
                Ver en Google Maps <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
              </a>
            </div>
          </div>
        </div>

        <!-- Lista de Servicios -->
        <div>
          <h4 class="text-xs font-bold uppercase tracking-wider text-slate-400 mb-3">
            Servicios que ofrece
          </h4>
          <div id="modalServices" class="flex flex-wrap gap-2">
            <!-- Etiquetas de servicios -->
          </div>
        </div>

        <!-- Botones de acción -->
        <div class="mt-8 pt-5 border-t border-slate-200 flex flex-wrap justify-end gap-3">
          <button
            onclick="closeDetailModal()"
            class="px-5 py-2.5 rounded-lg border border-slate-300 text-slate-700 font-medium text-sm hover:bg-slate-50 transition cursor-pointer"
          >
            Cerrar
          </button>
          <a
            id="modalCallAction"
            href="#"
            class="px-5 py-2.5 rounded-lg bg-navy-900 hover:bg-navy-800 text-white font-semibold text-sm transition flex items-center gap-2"
          >
            <i class="fa-solid fa-phone-volume text-amber-400"></i> Llamar Ahora
          </a>
        </div>
      </div>
    </div>
  </div>

  <!-- ==========================================
       MODAL 2: REGISTRAR NUEVO NEGOCIO
  =========================================== -->
  <div id="registerModal" class="fixed inset-0 z-50 hidden bg-navy-950/75 backdrop-blur-sm flex items-center justify-center p-4 overflow-y-auto">
    <div class="bg-white rounded-2xl max-w-xl w-full overflow-hidden shadow-2xl border border-slate-200 my-auto">
      <div class="bg-navy-900 text-white px-6 py-5 flex items-center justify-between border-b border-navy-800">
        <div>
          <h3 class="font-serif text-xl font-bold">Afiliar Nuevo Negocio</h3>
          <p class="text-xs text-slate-300">Completa los datos para publicar el comercio en el directorio</p>
        </div>
        <button onclick="closeRegisterModal()" class="text-slate-400 hover:text-white transition cursor-pointer">
          <i class="fa-solid fa-xmark text-lg"></i>
        </button>
      </div>

      <form id="registerForm" onsubmit="handleRegisterSubmit(event)" class="p-6 space-y-4">
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Nombre del Negocio *</label>
            <input
              type="text"
              id="regName"
              required
              placeholder="Ej. Panadería La Espiga"
              class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
            />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Categoría *</label>
            <select
              id="regCategory"
              required
              class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none bg-white"
            >
              <option value="Gastronomía">Gastronomía</option>
              <option value="Tecnología">Tecnología</option>
              <option value="Salud y Bienestar">Salud y Bienestar</option>
              <option value="Construcción y Hogar">Construcción y Hogar</option>
              <option value="Servicios Profesionales">Servicios Profesionales</option>
              <option value="Comercio Minorista">Comercio Minorista</option>
            </select>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Número de Teléfono *</label>
            <input
              type="tel"
              id="regPhone"
              required
              placeholder="Ej. +52 55 9876 5432"
              class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
            />
          </div>
          <div>
            <label class="block text-xs font-semibold text-slate-700 mb-1">Lugar donde se localiza *</label>
            <input
              type="text"
              id="regLocation"
              required
              placeholder="Ej. Av. Reforma 240, Col. Centro"
              class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
            />
          </div>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">Servicios (separados por coma) *</label>
          <input
            type="text"
            id="regServices"
            required
            placeholder="Ej. Pan artesanal, Cafetería, Pedidos para eventos, Envío a domicilio"
            class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
          />
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">Descripción breve del local</label>
          <textarea
            id="regDescription"
            rows="2"
            placeholder="Describe brevemente la trayectoria o especialidad del negocio..."
            class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
          ></textarea>
        </div>

        <div>
          <label class="block text-xs font-semibold text-slate-700 mb-1">
            Fotos del local (Sube archivos o pega URLs separadas por coma)
          </label>
          <input
            type="file"
            id="regPhotoFiles"
            accept="image/*"
            multiple
            class="w-full text-xs text-slate-500 file:mr-3 file:py-2 file:px-3 file:rounded-lg file:border-0 file:text-xs file:font-semibold file:bg-amber-50 file:text-amber-700 hover:file:bg-amber-100 mb-2 cursor-pointer"
          />
          <input
            type="text"
            id="regPhotoUrls"
            placeholder="O pega URLs de imágenes: https://ejemplo.com/foto1.jpg, https://..."
            class="w-full px-3.5 py-2 rounded-lg border border-slate-300 text-sm focus:ring-2 focus:ring-amber-500 focus:border-amber-500 outline-none"
          />
          <p class="text-[11px] text-slate-400 mt-1">Si no subes fotos, se asignará una imagen institucional por defecto.</p>
        </div>

        <div class="pt-4 border-t border-slate-200 flex justify-end gap-3">
          <button
            type="button"
            onclick="closeRegisterModal()"
            class="px-4 py-2 rounded-lg border border-slate-300 text-slate-700 text-sm font-medium hover:bg-slate-50 transition cursor-pointer"
          >
            Cancelar
          </button>
          <button
            type="submit"
            class="px-5 py-2 rounded-lg bg-amber-500 hover:bg-amber-400 text-navy-950 font-bold text-sm transition shadow-sm cursor-pointer"
          >
            Publicar Negocio
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Scripts de Lógica de la Aplicación -->
  <script>
    // Datos iniciales de ejemplo para la Cámara de Comercio
    const defaultBusinesses = [
      {
        id: 1,
        name: "Café & Tostaduría El Mirador",
        category: "Gastronomía",
        phone: "+52 55 4829 1034",
        location: "Av. Hidalgo #142, Zona Centro",
        description: "Cafetería de especialidad y tostaduría artesanal con granos seleccionados de altura. Un espacio ideal para reuniones ejecutivas y coworking.",
        services: ["Café de especialidad", "Desayunos ejecutivos", "Venta de grano tostado", "Catering empresarial", "Wi-Fi de alta velocidad"],
        photos: [
          "https://images.unsplash.com/photo-1554118811-1e0d58224f24?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1509042239860-f550ce710b93?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1497935586351-b67a49e012bf?auto=format&fit=crop&w=900&q=80"
        ]
      },
      {
        id: 2,
        name: "Soluciones Tecnológicas NovaTech",
        category: "Tecnología",
        phone: "+52 55 7391 2280",
        location: "Blvd. Empresarial #508, Local 12, Plaza Norte",
        description: "Consultoría informática, desarrollo de software a la medida y soporte técnico integral para pequeñas y medianas empresas.",
        services: ["Soporte técnico IT", "Desarrollo web y apps", "Redes y ciberseguridad", "Venta de equipo de cómputo", "Facturación electrónica"],
        photos: [
          "https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1531482615713-2afd69097998?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1519389950473-47ba0277781c?auto=format&fit=crop&w=900&q=80"
        ]
      },
      {
        id: 3,
        name: "Clínica Dental & Estética Sonrisa Real",
        category: "Salud y Bienestar",
        phone: "+52 55 6104 8821",
        location: "Calle Morelos #89, Col. Jardines",
        description: "Centro odontológico equipado con tecnología digital de última generación y especialistas certificados en rehabilitación oral.",
        services: ["Ortodoncia invisible", "Limpieza ultrasónica", "Implantes dentales", "Blanqueamiento láser", "Urgencias dentales"],
        photos: [
          "https://images.unsplash.com/photo-1629909613654-28e377c37b09?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1519494026892-80bbd2d6fd0d?auto=format&fit=crop&w=900&q=80"
        ]
      },
      {
        id: 4,
        name: "Ferretería y Materiales El Constructor",
        category: "Construcción y Hogar",
        phone: "+52 55 3920 4415",
        location: "Calzada Industrial #1240, Parque Sur",
        description: "Distribuidora mayorista y minorista de materiales para construcción, herramientas eléctricas, plomería y acabados arquitectónicos.",
        services: ["Materiales de obra", "Herramienta eléctrica", "Plomería y electricidad", "Entrega en obra sin costo", "Asesoría técnica"],
        photos: [
          "https://images.unsplash.com/photo-1581783898377-1c85bf937427?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1504307651254-35680f356dfd?auto=format&fit=crop&w=900&q=80"
        ]
      },
      {
        id: 5,
        name: "Despacho Contable y Fiscal Alianza",
        category: "Servicios Profesionales",
        phone: "+52 55 8450 1923",
        location: "Torre Ejecutiva Piso 4, Despacho 402, Av. Juárez",
        description: "Firma especializada en auditoría financiera, cumplimiento fiscal, gestión de nóminas y constitución de sociedades mercantiles.",
        services: ["Contabilidad general", "Declaraciones fiscales", "Gestión de nómina", "Auditoría financiera", "Registro de marcas"],
        photos: [
          "https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1556761175-5973dc0f32e7?auto=format&fit=crop&w=900&q=80"
        ]
      },
      {
        id: 6,
        name: "Boutique & Sastrería Elegancia Urbana",
        category: "Comercio Minorista",
        phone: "+52 55 2190 6754",
        location: "Paseo Comercial Las Fuentes, Local 18",
        description: "Confección a medida, trajes ejecutivos y moda contemporánea con telas importadas de alta durabilidad.",
        services: ["Sastrería a medida", "Ajustes y composturas", "Ropa ejecutiva", "Asesoría de imagen", "Uniformes corporativos"],
        photos: [
          "https://images.unsplash.com/photo-1441986300917-64674bd600d8?auto=format&fit=crop&w=900&q=80",
          "https://images.unsplash.com/photo-1507679799987-c73779587ccf?auto=format&fit=crop&w=900&q=80"
        ]
      }
    ];

    // Cargar negocios desde localStorage o usar los predeterminados
    let businesses = JSON.parse(localStorage.getItem('camara_comercio_negocios')) || defaultBusinesses;
    let currentCategory = 'Todos';

    // Inicializar vista
    document.addEventListener('DOMContentLoaded', () => {
      renderBusinesses(businesses);
    });

    // Renderizar tarjetas de negocios
    function renderBusinesses(list) {
      const grid = document.getElementById('businessGrid');
      const emptyState = document.getElementById('emptyState');
      const resultsCount = document.getElementById('resultsCount');

      grid.innerHTML = '';

      if (list.length === 0) {
        grid.classList.add('hidden');
        emptyState.classList.remove('hidden');
        resultsCount.textContent = '0 negocios encontrados';
        return;
      }

      grid.classList.remove('hidden');
      emptyState.classList.add('hidden');
      resultsCount.textContent = `Mostrando ${list.length} ${list.length === 1 ? 'negocio afiliado' : 'negocios afiliados'}`;

      list.forEach(biz => {
        const mainPhoto = biz.photos && biz.photos.length > 0
          ? biz.photos[0]
          : 'https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=900&q=80';

        const photoCountBadge = biz.photos && biz.photos.length > 1
          ? `<span class="absolute bottom-3 right-3 bg-navy-950/80 backdrop-blur-xs text-white text-xs px-2.5 py-1 rounded-md flex items-center gap-1.5">
               <i class="fa-solid fa-images text-amber-400"></i> ${biz.photos.length} fotos
             </span>`
          : '';

        const servicesBadges = biz.services.slice(0, 3).map(srv =>
          `<span class="bg-slate-100 text-slate-700 text-xs px-2.5 py-1 rounded-md font-medium">${srv}</span>`
        ).join('');

        const extraServicesCount = biz.services.length > 3
          ? `<span class="bg-amber-50 text-amber-700 border border-amber-200 text-xs px-2 py-1 rounded-md font-semibold">+${biz.services.length - 3} más</span>`
          : '';

        const card = document.createElement('article');
        card.className = 'bg-white rounded-2xl border border-slate-200/90 overflow-hidden shadow-sm card-hover flex flex-col justify-between';
        card.innerHTML = `
          <div>
            <!-- Foto del local -->
            <div class="relative h-52 w-full bg-slate-200 overflow-hidden cursor-pointer group" onclick="openDetailModal(${biz.id})">
              <img
                src="${mainPhoto}"
                alt="Local de ${biz.name}"
                class="w-full h-full object-cover group-hover:scale-105 transition duration-500"
                onerror="this.src='https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=900&q=80'"
              />
              <span class="absolute top-3 left-3 bg-navy-900/90 text-amber-400 text-xs font-semibold px-3 py-1 rounded-full shadow">
                ${biz.category}
              </span>
              ${photoCountBadge}
            </div>

            <!-- Contenido de la tarjeta -->
            <div class="p-5">
              <h3
                onclick="openDetailModal(${biz.id})"
                class="font-serif text-xl font-bold text-navy-900 mb-3 hover:text-amber-600 transition cursor-pointer line-clamp-1"
                title="${biz.name}"
              >
                ${biz.name}
              </h3>

              <!-- Teléfono y Lugar -->
              <div class="space-y-2 text-sm text-slate-600 mb-4">
                <div class="flex items-center gap-2.5">
                  <i class="fa-solid fa-phone text-amber-600 w-4 text-center"></i>
                  <a href="tel:${biz.phone.replace(/\s+/g, '')}" class="font-medium text-slate-800 hover:text-amber-600 transition">
                    ${biz.phone}
                  </a>
                </div>
                <div class="flex items-start gap-2.5">
                  <i class="fa-solid fa-location-dot text-amber-600 w-4 text-center mt-1"></i>
                  <span class="line-clamp-2 text-slate-600">${biz.location}</span>
                </div>
              </div>

              <!-- Servicios -->
              <div class="pt-3 border-t border-slate-100">
                <span class="text-[11px] font-bold uppercase tracking-wider text-slate-400 block mb-2">
                  Servicios principales
                </span>
                <div class="flex flex-wrap gap-1.5">
                  ${servicesBadges}
                  ${extraServicesCount}
                </div>
              </div>
            </div>
          </div>

          <!-- Pie de tarjeta -->
          <div class="px-5 py-3.5 bg-slate-50 border-t border-slate-100 flex items-center justify-between">
            <button
              onclick="openDetailModal(${biz.id})"
              class="text-navy-900 hover:text-amber-600 font-semibold text-sm flex items-center gap-1.5 transition cursor-pointer"
            >
              Ver local y detalles <i class="fa-solid fa-arrow-right text-xs"></i>
            </button>
            <a
              href="https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(biz.location)}"
              target="_blank"
              rel="noopener noreferrer"
              class="text-slate-400 hover:text-navy-900 transition text-sm"
              title="Abrir ubicación en mapa"
            >
              <i class="fa-solid fa-map-location-dot"></i>
            </a>
          </div>
        `;
        grid.appendChild(card);
      });
    }

    // Filtrar negocios por búsqueda y categoría
    function filterBusinesses() {
      const query = document.getElementById('searchInput').value.toLowerCase().trim();
      const selectCat = document.getElementById('categorySelect').value;
      const clearBtn = document.getElementById('clearSearchBtn');

      if (query.length > 0) {
        clearBtn.classList.remove('hidden');
      } else {
        clearBtn.classList.add('hidden');
      }

      currentCategory = selectCat;
      updateCategoryPills(selectCat);

      const filtered = businesses.filter(biz => {
        const matchesCat = selectCat === 'Todos' || biz.category === selectCat;
        const matchesText =
          biz.name.toLowerCase().includes(query) ||
          biz.location.toLowerCase().includes(query) ||
          biz.category.toLowerCase().includes(query) ||
          biz.services.some(s => s.toLowerCase().includes(query));

        return matchesCat && matchesText;
      });

      renderBusinesses(filtered);
    }

    function setCategory(cat) {
      document.getElementById('categorySelect').value = cat;
      filterBusinesses();
    }

    function updateCategoryPills(activeCat) {
      document.querySelectorAll('.cat-pill').forEach(pill => {
        if (pill.dataset.cat === activeCat) {
          pill.className = 'cat-pill active px-3.5 py-1.5 rounded-full text-xs font-semibold bg-navy-900 text-white transition cursor-pointer whitespace-nowrap';
        } else {
          pill.className = 'cat-pill px-3.5 py-1.5 rounded-full text-xs font-semibold bg-white text-slate-600 border border-slate-200 hover:border-navy-800 transition cursor-pointer whitespace-nowrap';
        }
      });
    }

    function clearSearch() {
      document.getElementById('searchInput').value = '';
      filterBusinesses();
    }

    function resetFilters() {
      document.getElementById('searchInput').value = '';
      document.getElementById('categorySelect').value = 'Todos';
      filterBusinesses();
    }

    // ==========================================
    // LÓGICA MODAL DETALLES DEL NEGOCIO
    // ==========================================
    function openDetailModal(id) {
      const biz = businesses.find(b => b.id === id);
      if (!biz) return;

      document.getElementById('modalCategory').textContent = biz.category;
      document.getElementById('modalName').textContent = biz.name;
      document.getElementById('modalDescription').textContent = biz.description || 'Comercio afiliado a nuestra Cámara de Comercio local.';
      document.getElementById('modalPhoneLink').textContent = biz.phone;
      document.getElementById('modalPhoneLink').href = `tel:${biz.phone.replace(/\s+/g, '')}`;
      document.getElementById('modalCallAction').href = `tel:${biz.phone.replace(/\s+/g, '')}`;
      document.getElementById('modalLocation').textContent = biz.location;
      document.getElementById('modalMapLink').href = `https://www.google.com/maps/search/?api=1&query=${encodeURIComponent(biz.location)}`;

      // Servicios
      const servicesContainer = document.getElementById('modalServices');
      servicesContainer.innerHTML = biz.services.map(srv =>
        `<span class="bg-navy-900/5 border border-navy-900/10 text-navy-900 text-xs sm:text-sm px-3 py-1.5 rounded-lg font-medium flex items-center gap-1.5">
           <i class="fa-solid fa-check text-amber-600 text-xs"></i> ${srv}
         </span>`
      ).join('');

      // Galería de Fotos del Local
      const photos = biz.photos && biz.photos.length > 0
        ? biz.photos
        : ['https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=900&q=80'];

      const mainImg = document.getElementById('modalMainImage');
      const counter = document.getElementById('modalPhotoCounter');
      const thumbsContainer = document.getElementById('modalThumbnails');

      mainImg.src = photos[0];
      counter.textContent = `Foto 1 de ${photos.length}`;
      thumbsContainer.innerHTML = '';

      if (photos.length > 1) {
        thumbsContainer.classList.remove('hidden');
        photos.forEach((photoUrl, index) => {
          const thumb = document.createElement('button');
          thumb.className = `w-16 h-12 rounded-md overflow-hidden border-2 shrink-0 transition cursor-pointer ${index === 0 ? 'border-amber-400 opacity-100' : 'border-transparent opacity-60 hover:opacity-100'}`;
          thumb.innerHTML = `<img src="${photoUrl}" class="w-full h-full object-cover" />`;
          thumb.onclick = () => {
            mainImg.src = photoUrl;
            counter.textContent = `Foto ${index + 1} de ${photos.length}`;
            Array.from(thumbsContainer.children).forEach((btn, i) => {
              btn.className = `w-16 h-12 rounded-md overflow-hidden border-2 shrink-0 transition cursor-pointer ${i === index ? 'border-amber-400 opacity-100' : 'border-transparent opacity-60 hover:opacity-100'}`;
            });
          };
          thumbsContainer.appendChild(thumb);
        });
      } else {
        thumbsContainer.classList.add('hidden');
      }

      document.getElementById('detailModal').classList.remove('hidden');
      document.body.style.overflow = 'hidden';
    }

    function closeDetailModal() {
      document.getElementById('detailModal').classList.add('hidden');
      document.body.style.overflow = '';
    }

    // ==========================================
    // LÓGICA MODAL REGISTRO DE NUEVO NEGOCIO
    // ==========================================
    function openRegisterModal() {
      document.getElementById('registerModal').classList.remove('hidden');
      document.body.style.overflow = 'hidden';
    }

    function closeRegisterModal() {
      document.getElementById('registerModal').classList.add('hidden');
      document.body.style.overflow = '';
    }

    function readFilesAsDataURLs(files) {
      const promises = Array.from(files).map(file => {
        return new Promise((resolve) => {
          const reader = new FileReader();
          reader.onload = (e) => resolve(e.target.result);
          reader.onerror = () => resolve(null);
          reader.readAsDataURL(file);
        });
      });
      return Promise.all(promises);
    }

    async function handleRegisterSubmit(event) {
      event.preventDefault();

      const name = document.getElementById('regName').value.trim();
      const category = document.getElementById('regCategory').value;
      const phone = document.getElementById('regPhone').value.trim();
      const location = document.getElementById('regLocation').value.trim();
      const servicesRaw = document.getElementById('regServices').value;
      const description = document.getElementById('regDescription').value.trim();
      const photoUrlsRaw = document.getElementById('regPhotoUrls').value;
      const photoFiles = document.getElementById('regPhotoFiles').files;

      const services = servicesRaw
        .split(',')
        .map(s => s.trim())
        .filter(s => s.length > 0);

      let photos = [];

      // Procesar archivos subidos
      if (photoFiles && photoFiles.length > 0) {
        const uploadedDataUrls = await readFilesAsDataURLs(photoFiles);
        photos.push(...uploadedDataUrls.filter(Boolean));
      }

      // Procesar URLs pegadas
      if (photoUrlsRaw.trim().length > 0) {
        const urls = photoUrlsRaw
          .split(',')
          .map(u => u.trim())
          .filter(u => u.startsWith('http'));
        photos.push(...urls);
      }

      // Imagen por defecto si no agregaron fotos
      if (photos.length === 0) {
        photos.push('https://images.unsplash.com/photo-1497366216548-37526070297c?auto=format&fit=crop&w=900&q=80');
      }

      const newBusiness = {
        id: Date.now(),
        name,
        category,
        phone,
        location,
        description: description || `Negocio afiliado en el sector de ${category}, ubicado en ${location}.`,
        services: services.length > 0 ? services : ['Atención personalizada'],
        photos
      };

      businesses.unshift(newBusiness);
      localStorage.setItem('camara_comercio_negocios', JSON.stringify(businesses));

      document.getElementById('registerForm').reset();
      closeRegisterModal();
      resetFilters();
    }

    // Cerrar modales con tecla Escape
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        closeDetailModal();
        closeRegisterModal();
      }
    });
  </script>
</body>
</html>
