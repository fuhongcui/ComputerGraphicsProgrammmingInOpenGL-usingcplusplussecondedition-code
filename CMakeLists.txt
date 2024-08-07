cmake_minimum_required(VERSION 3.0)

project(Main)

set(CMAKE_CXX_STANDARD 11)

include_directories(include)
link_directories(lib)

set(CHAPTERS
    Chapter_14_misc
    Chapter_13_geometry
    Chapter_17_stereoscopy
    Chapter_05_textures
    Chapter_08_shadows
    Chapter_06_models
    Chapter_02_opengl
    Chapter_07_lighting
    Chapter_15_water
    Chapter_12_tessellation
    Chapter_09_skybox
    Chapter_16_rayTracing
    Chapter_04_pipeline
    Chapter_10_bump
)

set(Chapter_14_misc
    Prog14_8_cloudsChanging
    Prog14_3_clipping
    Prog14_6_wood
    Prog14_7_clouds
    Prog14_2_blending
    Prog14_1_fog
    Prog14_9_dissolve
    Prog14_5_marble
    Prog14_4_stripes3Dtex
)

set(Chapter_13_geometry
    Prog13_2_geometryDel
    Prog13_4_geometryChange
    Prog13_1_1_geomModInflate
    Prog13_1_3_geomModExplodeWithBackFaces
    Prog13_1_2_geomModExplodeNoBackFaces
    Prog13_3_geometryAdd
)

set(Chapter_17_stereoscopy
    Prog17_2_sideBySide
    Prog17_1_anaglyph
    Prog17_3_distortionCorrection
)

set(Chapter_05_textures
    Prog5_1_texturedPyramid
    Prog5_1b_texturedPyramidMipmapAniso
)

set(Chapter_08_shadows
    Prog8_2_softShadowsPCF
    Prog8_1_shadowMapping
)

set(Chapter_06_models
    Prog6_2_torus
    Prog6_1_sphere
    Prog6_3_objLoaderShuttle
)

set(Chapter_02_opengl
    Prog2_supplemental_queryingOpenGL
    Prog2_1_background
    Prog2_6_animation
    Prog2_5_triangle
    Prog2_3_errorChecking
    Prog2_2_point
    Prog2_4_files
)

set(Chapter_07_lighting
    Prog7_1_lightingADS
)

set(Chapter_15_water
    Prog15_7_animation
    Prog15_8_caustics
    Prog15_2_geometry
    Prog15_1_surfaceSetup
    Prog15_4_noiseWaves
    Prog15_5+6_adjustments
    Prog15_3_reflectionRefraction
)

set(Chapter_12_tessellation
    Prog12_2_tessellationBezier
    Prog12_1_tessellationGridOnly
    Prog12_4_tessHeightMappedInstancedLOD
    Prog12_3_2_tessHeightMappedInstWLighting
    Prog12_3_1_tessHeightMappedInstanced
)

set(Chapter_09_skybox
    Prog9_3_environmentMapping
    Prog9_2_skyboxOpenGL
    Prog9_1_skyboxSimple
)

set(Chapter_16_rayTracing
    Prog16_8_plane
    Prog16_2_rayCasting
    Prog16_6_texture
    Prog16_11_combiningReflectionRefraction
    Prog16_3+4_lightingShadows
    Prog16_10_singleRefraction
    Prog16_9_singleReflection
    Prog16_12_recursion
    Prog16_7_skybox
    Prog16_1_computeShader
    Prog16_5_nonAxisBox
    Prog16_13+14+15+16_objectDefinition
)

set(Chapter_04_pipeline
    Prog4_1_3_tumbling
    Prog4_1_1_plainRedCube
    Prog4_4_matrixStack
    Prog4_2_instancing
    Prog4_3_multipleModels
    Prog4_1_2_interpolatedColors
    Prog4_1_4_multipleCubes
)

set(Chapter_10_bump
    Prog10_1_procBump
    Prog10_4_2_sphereVertexHeightMap
    Prog10_2_normalMapping
    Prog10_4_1_heightMappedTerrain
    Prog10_3_texturePlusNormal
)


function(create_project_from_sources chapter demo)
	file(GLOB SOURCE
            "src/${chapter}/${demo}/*.h"
            "src/${chapter}/${demo}/*.cpp"
        )
    set(NAME "${chapter}__${demo}")
    add_executable(${NAME} ${SOURCE})
    target_link_libraries(${NAME} GLEW glfw soil2-debug GL)
    set_target_properties(${NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin/${chapter}/${demo}")
    file(GLOB SHADERS
             "src/${chapter}/${demo}/*.glsl"
    )
    foreach(SHADER ${SHADERS})
            file(COPY ${SHADER} DESTINATION ${CMAKE_SOURCE_DIR}/bin/${chapter}/${demo})
    endforeach(SHADER)
endfunction()

foreach(CHAPTER ${CHAPTERS})
    foreach(DEMO ${${CHAPTER}})
		create_project_from_sources(${CHAPTER} ${DEMO})
    endforeach(DEMO)
endforeach(CHAPTER)
