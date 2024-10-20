# Construindo-uma-API-Rest-de-Consulta-de-Cidades-do-Brasil-do-Zero-at-a-Produ-o
src
└── main
    ├── java
    │   └── com
    │       └── exemplo
    │           └── cidades
    │               ├── CidadesApplication.java
    │               ├── controller
    │               │   └── CidadeController.java
    │               ├── model
    │               │   └── Cidade.java
    │               └── repository
    │                   └── CidadeRepository.java
    └── resources
        ├── application.properties
package com.exemplo.cidades;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class CidadesApplication {
    public static void main(String[] args) {
        SpringApplication.run(CidadesApplication.class, args);
    }
}
package com.exemplo.cidades.model;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Cidade {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nome;
    private String estado;

    // Getters e Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getEstado() {
        return estado;
    }

    public void setEstado(String estado) {
        this.estado = estado;
    }
}
package com.exemplo.cidades.repository;

import com.exemplo.cidades.model.Cidade;
import org.springframework.data.jpa.repository.JpaRepository;

public interface CidadeRepository extends JpaRepository<Cidade, Long> {
    // Métodos personalizados podem ser adicionados aqui
}
package com.exemplo.cidades.controller;

import com.exemplo.cidades.model.Cidade;
import com.exemplo.cidades.repository.CidadeRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/cidades")
public class CidadeController {

    @Autowired
    private CidadeRepository cidadeRepository;

    @GetMapping
    public List<Cidade> listarCidades() {
        return cidadeRepository.findAll();
    }

    @PostMapping
    public Cidade adicionarCidade(@RequestBody Cidade cidade) {
        return cidadeRepository.save(cidade);
    }
}
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.hibernate.ddl-auto=create
