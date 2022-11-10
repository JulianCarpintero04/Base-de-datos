-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema BaseDeDatosFinal
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema BaseDeDatosFinal
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `BaseDeDatosFinal` DEFAULT CHARACTER SET utf8 ;
USE `BaseDeDatosFinal` ;

-- -----------------------------------------------------
-- Table `BaseDeDatosFinal`.`usuario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `BaseDeDatosFinal`.`usuario` (
  `id` INT NOT NULL,
  `email` VARCHAR(45) NOT NULL,
  `usuariocol` VARCHAR(45) NOT NULL,
  `soyadmin` TINYINT NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `BaseDeDatosFinal`.`curso`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `BaseDeDatosFinal`.`curso` (
  `id` INT NOT NULL,
  `desarrollo` VARCHAR(200) NOT NULL,
  `url` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `BaseDeDatosFinal`.`proyecto`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `BaseDeDatosFinal`.`proyecto` (
  `id` INT NOT NULL,
  `desarrollo` VARCHAR(200) NOT NULL,
  `url` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`id`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `BaseDeDatosFinal`.`curso_has_usuario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `BaseDeDatosFinal`.`curso_has_usuario` (
  `curso_id` INT NOT NULL,
  `usuario_id` INT NOT NULL,
  PRIMARY KEY (`curso_id`, `usuario_id`),
  INDEX `fk_curso_has_usuario_usuario1_idx` (`usuario_id` ASC) VISIBLE,
  INDEX `fk_curso_has_usuario_curso_idx` (`curso_id` ASC) VISIBLE,
  CONSTRAINT `fk_curso_has_usuario_curso`
    FOREIGN KEY (`curso_id`)
    REFERENCES `BaseDeDatosFinal`.`curso` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_curso_has_usuario_usuario1`
    FOREIGN KEY (`usuario_id`)
    REFERENCES `BaseDeDatosFinal`.`usuario` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `BaseDeDatosFinal`.`proyecto_has_usuario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `BaseDeDatosFinal`.`proyecto_has_usuario` (
  `proyecto_id` INT NOT NULL,
  `usuario_id` INT NOT NULL,
  PRIMARY KEY (`proyecto_id`, `usuario_id`),
  INDEX `fk_proyecto_has_usuario_usuario1_idx` (`usuario_id` ASC) VISIBLE,
  INDEX `fk_proyecto_has_usuario_proyecto1_idx` (`proyecto_id` ASC) VISIBLE,
  CONSTRAINT `fk_proyecto_has_usuario_proyecto1`
    FOREIGN KEY (`proyecto_id`)
    REFERENCES `BaseDeDatosFinal`.`proyecto` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_proyecto_has_usuario_usuario1`
    FOREIGN KEY (`usuario_id`)
    REFERENCES `BaseDeDatosFinal`.`usuario` (`id`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
