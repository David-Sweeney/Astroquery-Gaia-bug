from astropy.coordinates import SkyCoord
from astropy import units as u
from astroquery.gaia import Gaia

Gaia.MAIN_GAIA_TABLE = "gaiadr3.gaia_source"
Gaia.ROW_LIMIT = -1

# Point 1 is my query point
point_1 = SkyCoord(ra=6.0285219922793285*u.deg,
                   dec=-72.27139628229959*u.deg)

# Point 2 is a source in Gaia
point_2 = SkyCoord(ra=5.996355959171072*u.deg, 
                   dec=-72.27528553257041*u.deg)

# The separation is ~38 arcsec
print(f"Separation between points: {point_1.separation(point_2).to(u.arcsec):.1f}")

# If we use astroquery to search Gaia for sources within 3 arcminutes of Point 1 we don't receive Point 2
radius = u.Quantity(3, u.arcmin)
r = Gaia.query_object(point_1, width=radius, height=radius)
found_object = bool(sum(abs(r['ra'] - point_2.ra) < 1e-5))
print(f"Object found with 3 arcminute search? {found_object}")

# If we do the same query for 4 arcminutes we see point 2
radius = u.Quantity(4, u.arcmin)
r = Gaia.query_object(point_1, width=radius, height=radius)
found_object = bool(sum(abs(r['ra'] - point_2.ra) < 1e-5))
print(f"Object found with 4 arcminute search? {found_object}")

# This problem does not affect the cone search
radius = u.Quantity(38, u.arcsec)
j = Gaia.cone_search(point_1, radius=radius)
r = j.get_results()
found_object = bool(sum(abs(r['ra'] - point_2.ra) < 1e-5))
print(f"Object found via 38 arcsec cone search? {found_object}")
