---
layout: page
title: Resources
permalink: /resources/
full_width: true
---

<div class="container py-5 mt-5">
    
    <!-- Hero Section -->
    <div class="text-center mb-5 pb-4 fade-in-up">
        <span class="badge bg-white bg-opacity-10 text-white border border-white border-opacity-25 rounded-pill mb-3 px-3 py-2">KNOWLEDGE BASE</span>
        <h1 class="display-3 fw-bold mb-3"><span class="text-brand">Curated Resources</span></h1>
        <p class="text-muted mx-auto lead" style="max-width: 600px;">
            Handpicked roadmaps, documentation, and archives to accelerate your learning journey.
        </p>
    </div>

    <div class="row g-4">
        <!-- Sidebar Filter (Sticky) -->
        <div class="col-lg-3 d-none d-lg-block">
            <div class="glass-card rounded-4 p-4 sticky-top" style="top: 100px;">
                <h6 class="text-white fw-bold mb-3 text-uppercase small opacity-50 ls-1">Navigate</h6>
                <div class="nav flex-column gap-2">
                    <a href="#roadmaps" class="nav-link text-white fw-bold ps-3 border-start border-2 border-brand bg-white bg-opacity-10 rounded-end">Roadmaps</a>
                    <a href="#docs" class="nav-link text-muted ps-3 hover-text-white transition-all">Quick Refs</a>
                    <a href="#archives" class="nav-link text-muted ps-3 hover-text-white transition-all">Archives</a>
                </div>
            </div>
        </div>

        <!-- Main Content -->
        <div class="col-lg-9">
            
            <!-- Roadmaps -->
            <div id="roadmaps" class="mb-5 fade-in-up">
                <div class="d-flex align-items-center mb-4">
                    <div class="icon-square bg-brand bg-opacity-10 text-brand rounded-circle p-3 me-3">
                        <i class="fas fa-map-signs fa-lg"></i>
                    </div>
                    <div>
                        <h3 class="fw-bold text-white mb-0">Learning Paths</h3>
                        <p class="text-muted small mb-0">Structured guides to master new tech.</p>
                    </div>
                </div>

                <div class="row g-4">
                    {% for map in site.data.resources.roadmaps %}
                    <div class="col-md-12">
                        <div class="glass-card p-4 rounded-4 h-100 position-relative overflow-hidden group">
                            <div class="row align-items-center">
                                <div class="col-md-8">
                                    <div class="d-flex gap-2 mb-2">
                                        <span class="badge bg-black border border-secondary text-white">{{ map.tag }}</span>
                                        <span class="badge bg-black border border-secondary text-muted"><i class="far fa-clock me-1"></i> {{ map.duration }}</span>
                                    </div>
                                    <h3 class="fw-bold text-white mb-2">{{ map.title }}</h3>
                                    <p class="text-muted mb-0">{{ map.description }}</p>
                                </div>
                                <div class="col-md-4 text-md-end mt-3 mt-md-0">
                                    <a href="{{ map.link }}" class="btn btn-brand rounded-pill px-4 fw-bold">Start Journey <i class="fas fa-arrow-right ms-2"></i></a>
                                </div>
                            </div>
                        </div>
                    </div>
                    {% endfor %}
                </div>
            </div>

            <!-- Docs / Quick Refs -->
            <div id="docs" class="mb-5 fade-in-up" style="animation-delay: 0.2s;">
                 <div class="d-flex align-items-center mb-4">
                    <div class="icon-square bg-info bg-opacity-10 text-info rounded-circle p-3 me-3">
                        <i class="fas fa-book-open fa-lg"></i>
                    </div>
                    <div>
                        <h3 class="fw-bold text-white mb-0">Quick References</h3>
                        <p class="text-muted small mb-0">Cheatsheets and official docs.</p>
                    </div>
                </div>
                
                <div class="row g-3">
                    {% if site.data.resources.docs.size > 0 %}
                        {% for tool in site.data.resources.docs %}
                        <div class="col-md-4 col-sm-6">
                            <a href="{{ tool.link }}" class="text-decoration-none">
                                <div class="glass-card p-4 rounded-4 h-100 d-flex flex-column align-items-center justify-content-center text-center hover-border-brand">
                                    <div class="bg-white bg-opacity-10 rounded-circle p-3 mb-3">
                                        <span class="fw-bold text-white">{{ tool.tag }}</span>
                                    </div>
                                    <h6 class="fw-bold text-white mb-1">{{ tool.title }}</h6>
                                    <small class="text-muted">{{ tool.subtitle }}</small>
                                </div>
                            </a>
                        </div>
                        {% endfor %}
                    {% else %}
                        <div class="col-12">
                            <div class="glass-card p-4 rounded-4 text-center text-muted">
                                <i class="fas fa-hammer mb-2"></i>
                                <p class="mb-0">Yet to be updated</p>
                            </div>
                        </div>
                    {% endif %}
                </div>
            </div>
            
            <!-- Archives Table -->
            <div id="archives" class="fade-in-up" style="animation-delay: 0.3s;">
                <div class="d-flex align-items-center mb-4">
                    <div class="icon-square bg-warning bg-opacity-10 text-warning rounded-circle p-3 me-3">
                        <i class="fas fa-box-archive fa-lg"></i>
                    </div>
                    <div>
                        <h3 class="fw-bold text-white mb-0">Archives</h3>
                        <p class="text-muted small mb-0">Past event materials and resources.</p>
                    </div>
                </div>

                <div class="glass-card rounded-4 overflow-hidden">
                    <div class="table-responsive">
                        <table class="table table-dark table-hover mb-0 align-middle" style="--bs-table-bg: transparent;">
                            <thead class="bg-black bg-opacity-25">
                                <tr>
                                    <th class="p-3 ps-4 text-uppercase text-muted small fw-bold border-0">Resource</th>
                                    <th class="p-3 text-uppercase text-muted small fw-bold border-0">Date</th>
                                    <th class="p-3 text-end pe-4 text-uppercase text-muted small fw-bold border-0">Action</th>
                                </tr>
                            </thead>
                            <tbody class="border-top-0">
                                {% if site.data.resources.archives.size > 0 %}
                                    {% for item in site.data.resources.archives %}
                                    <tr class="border-secondary border-opacity-10">
                                        <td class="p-3 ps-4 border-0">
                                            <div class="d-flex flex-column">
                                                <span class="text-white fw-bold">{{ item.title }}</span>
                                                <span class="text-muted small">{{ item.domain }}</span>
                                            </div>
                                        </td>
                                        <td class="p-3 text-muted small border-0">{{ item.date }}</td>
                                        <td class="p-3 text-end pe-4 border-0">
                                            <a href="{{ item.link }}" class="btn btn-sm btn-outline-secondary rounded-pill px-3">{{ item.action }}</a>
                                        </td>
                                    </tr>
                                    {% endfor %}
                                {% else %}
                                    <tr class="border-secondary border-opacity-10">
                                        <td colspan="3" class="p-5 text-center text-muted border-0">
                                            <i class="fas fa-clock mb-2 d-block"></i>
                                            Yet to be updated
                                        </td>
                                    </tr>
                                {% endif %}
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

        </div>
    </div>
</div>
