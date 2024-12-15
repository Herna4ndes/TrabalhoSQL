-- Criação da tabela "alunos"
CREATE TABLE alunos (
    id_aluno INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    endereco VARCHAR(255),
    telefone VARCHAR(15),
    email VARCHAR(100),
    data_nascimento DATE
);

-- Criação da tabela "cursos"
CREATE TABLE cursos (
    id_curso INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    duracao INT NOT NULL
);

-- Criação da tabela "materias"
CREATE TABLE materias (
    id_materia INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    codigo VARCHAR(10) UNIQUE NOT NULL,
    carga_horaria INT NOT NULL
);

-- Criação da tabela "professores"
CREATE TABLE professores (
    id_professor INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cpf VARCHAR(11) UNIQUE NOT NULL,
    especializacao VARCHAR(100) NOT NULL
);

-- Criação da tabela "turmas"
CREATE TABLE turmas (
    id_turma INT AUTO_INCREMENT PRIMARY KEY,
    codigo VARCHAR(10) UNIQUE NOT NULL,
    id_curso INT,
    id_materia INT,
    id_professor INT,
    semestre VARCHAR(6) NOT NULL,
    FOREIGN KEY (id_curso) REFERENCES cursos(id_curso),
    FOREIGN KEY (id_materia) REFERENCES materias(id_materia),
    FOREIGN KEY (id_professor) REFERENCES professores(id_professor)
);

-- Criação da tabela "notas"
CREATE TABLE notas (
    id_nota INT AUTO_INCREMENT PRIMARY KEY,
    id_aluno INT,
    id_turma INT,
    nota DECIMAL(5, 2) NOT NULL,
    FOREIGN KEY (id_aluno) REFERENCES alunos(id_aluno),
    FOREIGN KEY (id_turma) REFERENCES turmas(id_turma)
);

-- Criação de índices para otimizar o desempenho em buscas frequentes
CREATE INDEX idx_cpf_aluno ON alunos(cpf);
CREATE INDEX idx_codigo_materia ON materias(codigo);
CREATE INDEX idx_codigo_turma ON turmas(codigo);
CREATE INDEX idx_cpf_professor ON professores(cpf);
CREATE INDEX idx_id_aluno_nota ON notas(id_aluno);
CREATE INDEX idx_id_turma_nota ON notas(id_turma);
