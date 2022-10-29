-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema PortafolioWeb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema PortafolioWeb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `PortafolioWeb` DEFAULT CHARACTER SET utf8 ;
USE `PortafolioWeb` ;

-- -----------------------------------------------------
-- Table `PortafolioWeb`.`contenido`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `PortafolioWeb`.`contenido` (
  `id` INT NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `PortafolioWeb`.`usuario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `PortafolioWeb`.`usuario` (
  `id` INT NOT NULL,
  `email` VARCHAR(45) NOT NULL,
  `contraseña` VARCHAR(45) NOT NULL,
  `contenido_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_usuario_contenido_idx` (`contenido_id` ASC) VISIBLE,
  CONSTRAINT `fk_usuario_contenido`
    FOREIGN KEY (`contenido_id`)
    REFERENCES `PortafolioWeb`.`contenido` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `PortafolioWeb`.`proyecto`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `PortafolioWeb`.`proyecto` (
  `id` INT NOT NULL,
  `desarrollo` VARCHAR(200) NOT NULL,
  `url` VARCHAR(100) NULL,
  `contenido_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_proyecto_contenido1_idx` (`contenido_id` ASC) VISIBLE,
  CONSTRAINT `fk_proyecto_contenido1`
    FOREIGN KEY (`contenido_id`)
    REFERENCES `PortafolioWeb`.`contenido` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `PortafolioWeb`.`curso`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `PortafolioWeb`.`curso` (
  `id` INT NOT NULL,
  `desarrollo` VARCHAR(200) NOT NULL,
  `url` VARCHAR(100) NOT NULL,
  `contenido_id` INT NOT NULL,
  PRIMARY KEY (`id`),
  INDEX `fk_curso_contenido1_idx` (`contenido_id` ASC) VISIBLE,
  CONSTRAINT `fk_curso_contenido1`
    FOREIGN KEY (`contenido_id`)
    REFERENCES `PortafolioWeb`.`contenido` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `PortafolioWeb`.`administrador`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `PortafolioWeb`.`administrador` (
  `id` INT NOT NULL,
  `email` VARCHAR(45) NOT NULL,
  `contraseña` VARCHAR(45) NOT NULL,
  `modoeditor` TINYINT NOT NULL,
  `contenido_id` INT NOT NULL,
  PRIMARY KEY (`id`, `email`),
  INDEX `fk_administrador_contenido1_idx` (`contenido_id` ASC) VISIBLE,
  CONSTRAINT `fk_administrador_contenido1`
    FOREIGN KEY (`contenido_id`)
    REFERENCES `PortafolioWeb`.`contenido` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
