## Activate project renv when running notebooks in this subdirectory
project_root <- normalizePath("..", mustWork = TRUE)

# Force renv to treat the parent as the project root, even when launched
# from this subdirectory (prevents a new renv dir being created here).
Sys.setenv(
  RENV_PROJECT = project_root,
  RENV_PATHS_LIBRARY = file.path(project_root, "renv", "library")
)

activate <- file.path(project_root, "renv", "activate.R")
if (file.exists(activate)) {
  source(activate)
}
